# d3-star-plot

`d3.starPlot()` is designed to be a
[reusable](http://bost.ocks.org/mike/chart/) chart generator with sane
defaults and the necessary customization options. It encourages familiar
d3 design patterns to make building a series of star plots simple.

    var star = d3.starPlot()
      .accessors([
        function(d) { return scale(d.Body); },
        function(d) { return scale(d.Sweetness); },
        function(d) { return scale(d.Smokey); }
      ])
      .labels([
        'Body',
        'Sweetness',
        'Smokey'
      ])

    data.forEach(function(d) {
      d3.select(body).append('svg')
        .datum(d)
        .call(star)
    });

## Example

[http://bl.ocks.org/kevinschaul/8213691](Old demo)

To run the included example locally:

    $ npm install
    $ grunt

Open [http://0.0.0.0:8000](http://0.0.0.0:8000) in your browser.

## Downloads

- [d3-star-plot-0.0.0.min.js](https://raw.github.com/kevinschaul/d3-star-plot/master/dist/d3-star-plot-0.0.0.min.js)

## API

d3.**starPlot**()

Constructs a new star plot. The returned function generates svg elements
to create a star plot, including axis lines, labels, an origin circle
and the star plot path according to the associated data.

    var star = d3.starPlot();

star.**accessors**([accessors])

If `accessors` is specificed, sets the accessor functions for the
specified star plot.  If `accessors` is not specificed, returns the
current accessor functions. These must be set for the returned star plot
generator to produce a worthwhile chart.

`accessors` must be an array of accessor functions for the star
plot's associated data. The numbers should be scaled to fit in the
range `[0, 100]`. The order of `accessors` determines the clockwise
order of attributes to be drawn with the returned star plot generator.

    star.accessors([
      function(d) { return scale(d.Body); },
      function(d) { return scale(d.Sweetness); },
      function(d) { return scale(d.Smokey); }
    ]);

star.**labels**([labels])

If `labels` is specificed, sets the attriute labels for the
specified star plot.  If `labels` is not specificed, returns the
current labels. This value is optional.

`labels` must be an array of strings in the order that the corresponding
accessor functions are in.

    star.labels([
      'Body',
      'Sweetness',
      'Smokey'
    ]);

star.**labelMargin**([m])

If `m` is specificed, sets the margin of the specified star plot. If `m`
is not specificed, returns the current label margin value. This value is
used to place data labels farther from the origin. The default value is
`20`.

    star.labelMargin(20);

star.**width**([w])

If `w` is specificed, sets the width of the specified star plot. If `w`
is not specificed, returns the current width value. Because star plots
are square, the width value is also used for the height of the star
plot. The default value is `200`.

    star.width(200);

star.**margin**([m])

If `m` is specificed, sets the margin of the specified star plot. If `m`
is not specificed, returns the current margin value. `m` must be an
object with `top`, `right`, `bottom` and `left` properties.  By default,
these values are all `0`.

    var m = {
      top: 0,
      right: 0,
      bottom: 0,
      left: 0
    };
    star.margin(m);

star.**includeGuidelines**([boolean])

If `boolean` is specificed, sets the value. If `boolean`
is not specificed, returns the current label margin value. If this value
is true, the returned star plot generator will include lines from the
origin to the value of each of the data's attributes. The default value
is `true`.

    star.includeGuidelines(true);

star.**title**([title])

If `title` is specificed, sets the title accessor function of the
specified star plot. If `title` is not specificed, returns the current
title accessor function. The value returned by this function is used by
the returned star plot generator to label the chart.

    star.title(function(d) { return d.Distillery; });

