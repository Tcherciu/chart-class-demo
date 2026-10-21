<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
</head>
<body>
  <h1>hello</h1>
  <canvas id="chart" width="700" height="400"></canvas>

<script>
  const labels = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"];
  const data   = [12.00, 13.00, 10.00, 16.00, 18.00];

  const c = document.getElementById("chart");
  const g = c.getContext("2d");
  const padL = 60, padB = 50, padT = 30, padR = 30;
  const w = c.width - padL - padR;
  const h = c.height - padT - padB;
  const max = Math.max(...data) * 1.1;

  // axes
  g.strokeStyle = "#999";
  g.beginPath();
  g.moveTo(padL, padT);
  g.lineTo(padL, padT + h);
  g.lineTo(padL + w, padT + h);
  g.stroke();

  // points
  const pts = data.map((v, i) => [
    padL + (i * w) / (data.length - 1),
    padT + h - (v / max) * h
  ]);

  // line
  g.strokeStyle = "#FF0145";
  g.lineWidth = 3;
  g.beginPath();
  pts.forEach(([x, y], i) => i ? g.lineTo(x, y) : g.moveTo(x, y));
  g.stroke();

  // dots + labels
  g.fillStyle = "#FF0145";
  pts.forEach(([x, y]) => {
    g.beginPath();
    g.arc(x, y, 4, 0, Math.PI * 2);
    g.fill();
  });

  g.fillStyle = "#333";
  g.font = "12px sans-serif";
  g.textAlign = "center";
  pts.forEach(([x], i) => g.fillText(labels[i], x, padT + h + 20));
</script>
</body>
</html>
