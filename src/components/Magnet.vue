<template>
  <div class="magnet">
    <img src="@/assets/compass.svg" id="compass" class="compass"/>
    <br><br>
    <div id="status"></div>
  </div>
</template>

<script>
export default {
  name: 'Magnet',

  data() {
    return {
      magSensor: {}
    }
  },

  mounted() {
    let compass = document.getElementById('compass');
    let status  = document.getElementById('status');

    if ( 'AbsoluteOrientationSensor' in window ) {
      compass.hidden = false;     
      let sensor = new AbsoluteOrientationSensor();
      sensor.addEventListener('reading', function(e) {
        let q = e.target.quaternion;
        let heading = Math.atan2(2*q[0]*q[1] + 2*q[2]*q[3], 1 - 2*q[1]*q[1] - 2*q[2]*q[2])*(180/Math.PI);

        let html =  'Heading in degrees: ' + heading;
        if(heading < 0) heading = 360+heading;
        html += '<br>Adjusted:   ' + heading;
        status.innerHTML = html;
        compass.style.Transform = 'rotate(' + heading + 'deg)';
        compass.style.WebkitTransform = 'rotate('+ heading + 'deg)';
        compass.style.MozTransform = 'rotate(' + heading + 'deg)';
      });
      sensor.start();
    }
    else status.innerHTML = 'AbsoluteOrientationSensor not supported';

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.magnet {
  display: flex;
  height: 80vh;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  width: 100%;
}
.compass {
  width: 80%;
  max-width: 300px;
  transition: 0.08s all ease-in-out;
}

</style>
