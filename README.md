Rendered site at https://stephenturner.github.io/gi2017software

Data collected by Sean Davis: https://gist.github.com/seandavi/0b20c492527b234912ba2350a05cb10c

Code to generate site from https://github.com/derekeder/csv-to-html-table

### Usage

1. Clone this repo. 
2. Add your CSV file to the `data/` folder
3. In `index.html` set your options in the `CsvToHtmlTable.init()` function
``` html
<script>
  CsvToHtmlTable.init({
    csv_path: 'data/tcga.csv', 
    element: 'table-container', 
    allow_download: true,
    csv_options: {separator: ',', delimiter: '"'},
    datatables_options: {"paging": false}
  });
</script>
```
4. Run it with `python -m http.server`, and navigate to http://localhost:8000/.


### Available options

* `csv_path` Path to your CSV file.
* `element` The HTML element to render your table to. Defaults to `table-container`
* `allow_download` if true, shows a link to download the CSV file. Defaults to `false`
* `csv_options` jQuery CSV configuration. Use this if you want to use a custom `delimiter` or `separator` in your input file. See [their documentation](https://code.google.com/p/jquery-csv/wiki/API#$.csv.toArrays%28%29).
* `datatables_options` DataTables configuration. See [their documentation](http://datatables.net/reference/option/).
* `custom_formatting` A list of column indexes and custom functions to format your data (see below)

### Custom formatting

If you want to do custom formatting for one or more column, you can pass in an array of arrays containing the index of the column and a custom function for formatting it. You can pass in multiple formatters and they will be executed in order.

The custom functions must take in one parameter (the value in the cell) and return a string:

Example:

``` html
<script>

  //my custom function that creates a hyperlink
  function format_link(link){
    if (link)
      return "<a href='" + link + "' target='_blank'>" + link + "</a>";
    else
      return "";
  }

  //initializing the table
  CsvToHtmlTable.init({
    csv_path: 'data/Health Clinics in Chicago.csv', 
    element: 'table-container', 
    allow_download: true,
    csv_options: {separator: ',', delimiter: '"'},
    datatables_options: {"paging": false},
    custom_formatting: [[4, format_link]] //execute the function on the 4th column of every row
  });
</script>
```

### iframe

Want to embed your nifty table on your website? You can use an [iframe](http://www.w3schools.com/tags/tag_iframe.asp). Once you've deployed your table (above in step 5) you can link to it in an iframe right in your HTML.

```html
<iframe style="border-style: none;" src="http://stephenturner.github.io/tcga-codes/" height="950" width="600"></iframe>
```

### Dependencies

* [Bootstrap](http://getbootstrap.com/) - Responsive HTML, CSS and Javascript framework
* [jQuery](https://jquery.com/) - a fast, small, and feature-rich JavaScript library
* [jQuery CSV](https://github.com/evanplaice/jquery-csv/) - Parse CSV (Comma Separated Values) to Javascript arrays or dictionaries.
* [DataTables](http://datatables.net/) - add advanced interaction controls to any HTML table.

