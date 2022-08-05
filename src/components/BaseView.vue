<script>
export default {
  name: 'BaseView',
  props: {
    msg: String,
    img: String,
    alt: String,
    color: String
  },
  methods: {
     getImg(img) {
       return require(`../assets/${img}`);
     },
     getColor(color) {
       return {'background-color':color}
     }
   }
}
</script>
<style>
.baseview {
  width:100%;
  max-width: 800px;
  margin: auto;
  padding: 0;
  display: table;
}
</style>