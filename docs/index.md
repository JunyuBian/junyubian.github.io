---
hide:
    - date
home: true
template: home.html
statistics: true
---

# Hi there!

This is my site. 

Theme credits to TonyCrane, thanks Tony!

[:octicons-info-16: About](about/) / 
[:material-clock-time-two-outline: ChangeLog](changelog/) / 
[:material-chart-line: Statistics](javascript:toggle_statistics();)

<div id="statistics" markdown="1" class="card" style="width: 27em; border-color: transparent; opacity: 0; font-size: 75%">
<div style="padding-left: 1em;" markdown="1">
Pages: {{pages}}  
Words: {{words}}  
Code Blocks: {{codes}}  
Up Time: <span id="web-time"></span>
</div>
</div>

<script>
function updateTime() {
    var date = new Date();
    var now = date.getTime();
    var startDate = new Date("2022/01/03 09:10:00");
    var start = startDate.getTime();
    var diff = now - start;
    var y, d, h, m;
    y = Math.floor(diff / (365 * 24 * 3600 * 1000));
    diff -= y * 365 * 24 * 3600 * 1000;
    d = Math.floor(diff / (24 * 3600 * 1000));
    h = Math.floor(diff / (3600 * 1000) % 24);
    m = Math.floor(diff / (60 * 1000) % 60);
    if (y == 0) {
        document.getElementById("web-time").innerHTML = d + "<span class=\"heti-spacing\"> </span>days<span class=\"heti-spacing\"> </span>" + h + "<span class=\"heti-spacing\"> </span>hrs<span class=\"heti-spacing\"> </span>" + m + "<span class=\"heti-spacing\"> </span>mins";
    } else {
        document.getElementById("web-time").innerHTML = y + "<span class=\"heti-spacing\"> </span>yrs<span class=\"heti-spacing\"> </span>" + d + "<span class=\"heti-spacing\"> </span>days<span class=\"heti-spacing\"> </span>" + h + "<span class=\"heti-spacing\"> </span>hrs<span class=\"heti-spacing\"> </span>" + m + "<span class=\"heti-spacing\"> </span>mins";
    }
    setTimeout(updateTime, 1000 * 60);
}
updateTime();
function toggle_statistics() {
    var statistics = document.getElementById("statistics");
    if (statistics.style.opacity == 0) {
        statistics.style.opacity = 1;
    } else {
        statistics.style.opacity = 0;
    }
}
</script>