<template>
  <body>
    <div class="items">
      <div class="item"
        v-for="item in jsonTimelineSorted"
        :key="item"
        >
        <div class="date">{{item.registered | changeDateType}}</div>
        <div class="info">
          <p class="full-name">{{item.name.first + " " + item.name.last}}</p>
          <p>{{item.about}}</p>
        </div>
      </div>
    </div>
  </body>
</template>

<script>
export default {
  name: "timeline",

  props: {
    jsonTimeline: Object,
  },

  computed: {
    jsonTimelineSorted: function() {
      var jsonTimeline = this.jsonTimeline;
      jsonTimeline.sort(function(a, b) {
        var dateA = new Date(a.registered);
        var dateB = new Date(b.registered);
        if(dateA < dateB) {
          return -1;
        }
        if(dateA > dateB) {
          return 1;
        }
          return 0;
      });
      return jsonTimeline;
    }
  },

  filters: {
    changeDateType: function(value) {
      value = new Date(value)
      return value.toDateString()
    }
  }
}

</script>
<style scoped lang="scss">
body {
  margin: 0;
  font-family: 'Droid Sans', sans-serif;
  &:before {
    content: '';
    position: fixed;
    top: 0px;
    left: 50%;
    bottom: 0px;
    transform: translateX(-50%);
    width: 4px;
    background-color: #1d1d1d;
  }
  .items {
    width: calc(100% - 80px);
    max-width: 800px;
    margin: auto;
    position: relative;
    left: -5px;
    .item {
      width: calc(50% - 80px);
      float: left;
      padding: 20px;
      clear: both;
      text-align: right;
      &:not(:first-child) {
        margin-top: -60px;
      }
      .date {
        font-size: 32px;
        margin-bottom: 12px;
        position: relative;
        color: #8dd9ab;
        &:before {
          content: '';
          position: absolute;
          width: 8px;
          height: 8px;
          border: 4px solid #8dd9ab;
          background-color: #1d1d1d;
          border-radius: 100%;
          top: 50%;
          transform: translateY(-50%);
          right: -73px;
          z-index: 1000;
        }
        &.big:before {
          width: 24px;
          height: 24px;
          transform: translate(8px,-50%);
        }
      }
      .info {
        color: #aaa;
        p {
          line-height: 1.4em;
        }
        .full-name {
          font-size: 20px;
        }
      }
      &:nth-child(2n) {
        text-align: left;
        float: right;
        .date {
          &:before {
            left: -63px;
          }
          &.big:before {
            transform: translate(-8px,-50%);
          }
        }
      }
    }
  }
}
</style>
