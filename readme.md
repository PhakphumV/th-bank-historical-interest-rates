# Python code to scrap historical interest rates data of each banks from bot.or.th

This is a jupyter notebook to extract historical interest rates of each commercial banks in Thailand since 31JAN1996 (31 ม.ค. 2539)

The [webpage](https://www.bot.or.th/thai/statistics/_layouts/application/interest_rate/in_historical.aspx) provide historical interest rates per day of selected bank and given date range either in XLS format or CSV format. However, the date range is limited to 1 year and a single bank can be selected at a time.

## Objective
To automate data extraction from this webpage in order to extract all different commercial banks in Thailand and data from 31JAN1996 into a consolidated format.

## Assessment
// Done on 13JAN2023

Found that the download button is using Javascript as following

```
<a href="#" onclick="downloadFile('interestXLS')" class="app_table_content_link">...</a>
<a href="#" onclick="downloadFile('interestCSV')" class="app_table_content_link">...</a>
```

And this ```downloadFile``` function works as following

1. Retrieve inputs such as dateFrom, dateTo, bankId, bankName and an option to select whether to extract interest rate for deposit or loan
2. Construct an url link with above params 
3. Open a tab to the url to start download a file corresponding to the inputs.

```
function downloadFile( dlType){
  var dateFrom = document.getElementById("ctl00_PlaceHolderMain_hdFDate").value;
  var dateTo = document.getElementById("ctl00_PlaceHolderMain_hdTDate").value;
  var ddlBank = document.getElementById("ctl00_PlaceHolderMain_ddlBank"); //option object
  var bankId = ddlBank.options[ddlBank.options.selectedIndex].value;
  var bankName = ddlBank.options[ddlBank.options.selectedIndex].text;
  var rdoDeposit = document.getElementById("ctl00_PlaceHolderMain_rdoType_0");
  var rdoType;
  if(rdoDeposit.checked){
      rdoType = 0;
  }else{
      rdoType = 1;
  }
var url = "./DownloadFile.aspx?dlType=" + dlType + "&dateFrom=" + dateFrom + "&dateTo=" + dateTo + "&bankValue=" + bankId + "&bankName=" + bankName + "&rdoTypeStr=" + rdoType;
//alert(url);
  window.location.href = url;
}
```


