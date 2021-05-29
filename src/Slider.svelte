<script>
    export let value = 24;
</script>
<style>

input[type="range"]{
  -webkit-appearance:none;
  width:10rem;
  height:20px;
  background: linear-gradient(to right, #1e56cf 0%, #1dce8a 100%);
  background-size:150px 10px;
  background-position:center;
  background-repeat:no-repeat;
  overflow:hidden;
  outline: none;
}

input[type="range"]::-webkit-slider-thumb{
  -webkit-appearance:none;
  width:20px;
  height:20px;
  cursor: pointer;
  border-radius: 50%;
  background:#979797;
  border: 2px solid rgb(31, 31, 31) ;
  position:relative;
  z-index:3;
  box-shadow:0 0 5px 0 rgba(0,0,0,0.3);
}

input[type="range"]::-webkit-slider-thumb:after{
  content:" ";
  width:160px;
  height:10px;
  position:absolute;
  z-index:1;
  background: #ff5b32;
  background: linear-gradient(to right, #f088fc 1%, #AC6CFF 70%);
}

</style>

<input class="unselectable" type="range" bind:value={value} />