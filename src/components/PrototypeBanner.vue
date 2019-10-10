<template>
    <div class="prototype-banner">
        <p class="prototype-text">
            This is a prototype.  Any information gained from this tool should be verified.
        </p>
    </div>
</template>

<script>

export default {
  name: 'PrototypeBanner',
  props: {
  },
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.prototype-banner {
    background-color: #FEC04F;
    width: 100%;
    position: absolute;
    top: 0;
    display: table;
}

.prototype-text {
  text-align:center; 
  vertical-align: middle;
  display: table-cell;
  padding: 10px;
  font-weight: bold;
}
</style>
