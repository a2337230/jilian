<template>
  <div class="select-container">
    <div class="select">
      <div class="select-item" @click="clickOne">
        <p>{{depData.Name}}</p>
      </div>
      <div class="select-child" v-for="(item, index) in dataChild" :key="item.CommonTypeID">
        <div class="select-froup">
          <p v-for="citem in item.Nodes" :key="citem.CommonTypeID" @click="clickChild(citem, index)">{{citem.Name}}</p>
        </div>
      </div>
    </div>
    <div class="select-btn">
      <div class="btn-froup">
        111
      </div>
    </div>
    <div class="share"></div>
  </div>
 
</template>

<script>
import dataMoke from './../../static/data.json'
export default {
  name: 'HelloWorld',
  data () {
    return {
      depData: dataMoke.Data[0],
      dataChild: '',
      checkItem: []
    }
  },
  mounted () {
    console.log(this.depData)
  },
  methods: {
    clickOne () {
      this.dataChild = []
      let data = {
        Nodes: this.depData.Nodes
      }
      this.dataChild.push(data)
    },
    clickChild (val, index) {
      let isNull = index + 1
      console.log(index, this.dataChild)
      // let parentBox = document.querySelector('.select')
      // parentBox.style.transform = `translateX(-${33.3 * index}vw)`
      if (val.Nodes.length === 0) {
        this.dataChild.splice(isNull)
        return
      }
      
      if (this.dataChild.length >= index + 2) {
        this.dataChild[index + 1].Nodes = val.Nodes
        if (this.dataChild.length !== index + 2) {
          let num = index + 2
          this.dataChild.length = num
        }
        
      } else {
        let data = {
          Nodes: val.Nodes
        }
        this.dataChild.push(data)
      }
      let parentBox = document.querySelector('.select')
      let container = document.querySelectorAll('.select-child')
      
      console.log(container.length, parentBox.offsetWidth)
    }
  },
  watch: {
    dataChild () {

    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.select-container {
  position: relative;
  width: 100vw;
  overflow-x: scroll;
}
.select {
  display: flex;
  transform: translateX(0);
  transition: .3s;
}
.select-item, .select-child {
  width: 33.3%;
  height: 7rem;
  
}
.select-item p, .select-child p {
  width: 33.3vw;
  font-size: .3rem;
  line-height: .5rem;
  color: #333;
}
.current p {
  color: blue;
}
.select-froup {
  height: 6.3rem;
  overflow-y: scroll;
}
.select-btn {
  position: relative;
}
.select-btn .btn-froup {
  position: absolute;
  left: 33.3vw;
}
.share {
  position: absolute;
  left: 0;
  top: 0;
  width: 33.3vw;
  height: 7rem;
  background-color: rgba(0,0,0,0.3);
  z-index: -1;
}
</style>
