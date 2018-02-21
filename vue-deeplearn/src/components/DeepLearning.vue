<template>
  <div class="deepLearning">hoge</div>
</template>

<script>
import * as dl from 'deeplearn'

export default {
  name: 'DeepLearning',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  mounted () {
    (async () => {
      const a = dl.variable(dl.scalar(Math.random()))
      const b = dl.variable(dl.scalar(Math.random()))
      const c = dl.variable(dl.scalar(Math.random()))

      const learningRate = 0.01
      const optimizer = dl.train.sgd(learningRate)

      const predict = input => {
        return dl.tidy(() => {
          const x = dl.scalar(input)
          const ax2 = a.mul(x.square())
          const bx = b.mul(x)
          const y = ax2.add(bx).add(c)
          return y
        })
      }

      const loss = (prediction, actual) => {
        const error = dl.scalar(actual).sub(prediction).square()
        return error
      }

      const train = async (xs, ys, numIterations, done) => {
        // let currentIteration = 0
        for (let iter = 0; iter < numIterations; iter++) {
          for (let i = 0; i < xs.length; i++) {
            optimizer.minimize(() => {
              const pred = predict(xs[i])
              const predLoss = loss(pred, ys[i])

              return predLoss
            })
          }
          await dl.nextFrame()
        }
        done()
      }

      const test = (xs, ys) => {
        dl.tidy(() => {
          const predictedYs = xs.map(predict)
          console.log('Expected', ys)
          console.log('Got', predictedYs.map(p => p.dataSync()[0]))
        })
      }

      const data = {
        xs: [0, 1, 2, 3],
        ys: [1.1, 5.9, 16.8, 33.9]
      }

      console.log('Before training: using random coefficients')
      test(data.xs, data.ys)
      train(data.xs, data.ys, 50, () => {
        console.log(
          `After training: a=${a.dataSync()}, b=${b.dataSync()}, c=${c.dataSync()}`
        )
        test(data.xs, data.ys)
      })
    })()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
