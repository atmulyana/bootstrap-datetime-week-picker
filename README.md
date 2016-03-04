# bootstrap-datetime/week picker
A datetime/week picker widget that can be used on a web page. This project is the modification and improvement of another project at
https://github.com/eternicode/bootstrap-datepicker/ <br/>version 1.4.0 which is developed by Andrew Rowls + contributors.

All documentation in http://bootstrap-datepicker.readthedocs.org/en/stable/ should apply to this project. Here will be explained
the modifications/extensions made in this project. There are three major features added to this project:
<ul>
  <li><h4>Different date format</h4>
    <p>This project uses <code>JsSimpleDateFormat</code> library which is developed by me. This library has wider formatting
       pattern including time that will be used by time picker. The formatting pattern used by this
       library is similar to that used by Java SimpleDateFormat class and also similar to .NET date time string format. If you
       use Java or ASP.NET as the server-side code, it's a benefit if we use the same format pattern between client and server.
    </p>
    <p>To use <code>JsSimpleDateFormat</code>, you must include <code>JsSimpleDateFormat.js</code> script before
       <code>bootstrap-datepicker.js</code>, like below:
       <pre>
          &lt;script src="./js/JsSimpleDateFormat.min.js"&gt;&lt;/script&gt;
          &lt;script src="./js/bootstrap-datepicker.min.js"&gt;&lt;/script&gt;</pre>
       If you omit <code>JsSimpleDateFormat.js</code>, datepicker will use the internal format pattern as described at<br/>
       http://bootstrap-datepicker.readthedocs.org/en/stable/options.html#format
    </p>
  </li>
  <li><h4>Week picker</h4>
    <p>Week picker is to select a whole week, instead of a single day. The
       <a href="http://bootstrap-datepicker.readthedocs.org/en/stable/options.html#weekstart"><code>weekstart</code></a>
       option determines the first day of the week. To use week picker, set <code>weekPicker</code> option to
       <code>true</code>. By default, it's <code>false</code>. The week will be displayed as
       <code style="white-space:nowrap">[first date of week][separator][last date of week]</code>. The default separator is
       hyphen (-). To use different seperator, set <code>weekPicker</code> option to an object whose <code>separator</code>
       property, such as:
       <pre>weekPicker: { separator: ' upto ' }</pre>
       Beside <code>separator</code> property, the object may have two methods: <code>formatWeek</code> and
       <code>getWeekStart</code>. <code>formatWeek</code> is to format the week more freely. It may ignore
       <code>separator</code> property. <code>getWeekStart</code> is to parse the string formatted by <code>formatWeek</code>
       and returns the first date of the week. For example, consider <code>weekstart</code> option is set to sunday, we can use
       the following code:
       <pre>
       weekPicker: {
          formatWeek: function(startWeekDate, options) {
            var df = new JsSimpleDateFormat("'Week-'W of MMM yyyy");
            return df.format(startWeekDate);
          },
          getWeekStart: function(weekString, options) {
            var df = new JsSimpleDateFormat("'Week-'W of MMM yyyy");
            df.isLenient = true;
            return df.parse(weekString);
          }
       }
       </pre>
    </p>
  </li>
  <li><h4>Time picker</h4>
    <p>Beside date, this widget can set time.  Some coditions in the use of time:
      <ul>
        <li>It must use <code>JsSimpleDateFormat</code>.</li>
        <li><code>weekPicker</code> and
            <a href="http://bootstrap-datepicker.readthedocs.org/en/stable/options.html#multidate"><code>multidate</code></a>
            option must be set to <code>false</code>.
        </li>
        <li>Time picker will appear if
            <a href="http://bootstrap-datepicker.readthedocs.org/en/stable/options.html#format">format</a> pattern
            includes <code>H</code>, <code>k</code>, <code>K</code>, <code>h</code>, <code>m</code> or <code>s</code>.
            These are the format pattern for time.
        </li>
        <li>If <code>s</code> is specified in format string then hour, minute and second picker will appear. If <code>m</code>
            is specified but no <code>s</code> then only hour and minute will appear. If no <code>m</code> and <code>s</code>
            is in format string then only hour will appear. The AM/PM button will appear if you use <code>K</code> or
            <code>h</code> in format string.
        </li>
        <li>If time picker appears then there is <code>nowBtn</code> option that can be used. It's like
            <a href="http://bootstrap-datepicker.readthedocs.org/en/stable/options.html#todaybtn"><code>todayBtn</code></a>
            except it will also set the time to the current time. The possible values for <code>nowBtn</code> are the same
            as those for <code>todayBtn</code> option.
        </li>
      </ul>
    </p>
  </li>
</ul>
