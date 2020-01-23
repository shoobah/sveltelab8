<script>
  export var time = Date();

  function findPoint(cx, cy, rad, cornerGrad) {
    var cornerRad = (cornerGrad * Math.PI) / 180;
    var nx = Math.cos(cornerRad) * rad + cx;
    var ny = Math.sin(cornerRad) * rad + cy;
    return { x: nx, y: ny };
  }

  function timeToDeg(time) {
    return (time / 60) * 360 - 90;
  }

  function hourToDeg(time) {
    return (time / 12) * 360 - 90;
  }

  var secPoint2 = findPoint(150, 150, 120, timeToDeg(0));
  var minPoint2 = findPoint(150, 150, 120, timeToDeg(0));
  var hourPoint2 = findPoint(150, 150, 120, timeToDeg(0));

  $: {
    console.log(
      "%c🖖" + new Date().toLocaleTimeString("se") + " time:",
      "color:lime",
      time
    );
    if (time) {
      secPoint2 = findPoint(150, 150, 144, timeToDeg(time.getSeconds()));
      minPoint2 = findPoint(150, 150, 120, timeToDeg(time.getMinutes()));
      hourPoint2 = findPoint(150, 150, 100, hourToDeg(time.getHours()));
    }
  }
</script>

<svg width="300" height="300">
  <circle
    cx="150"
    cy="150"
    r="148"
    fill="white"
    stroke-width="2"
    stroke="black" />
  <line
    x1="150"
    y1="150"
    x2={secPoint2.x}
    y2={secPoint2.y}
    stroke="red"
    stroke-width="2" />
  <line
    x1="150"
    y1="150"
    x2={minPoint2.x}
    y2={minPoint2.y}
    stroke="black"
    stroke-width="4" />
  <line
    x1="150"
    y1="150"
    x2={hourPoint2.x}
    y2={hourPoint2.y}
    stroke="black"
    stroke-width="4" />
</svg>
