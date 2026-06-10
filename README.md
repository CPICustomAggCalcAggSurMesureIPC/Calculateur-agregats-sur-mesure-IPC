
# CPIAggr 

The CPIAggr R package launches the CPI Custom Aggregate Calculator, an interactive app which allows users of Statistics Canada data to select published CPI geographies and products and calculate Custom CPIs as aggregates of the selected series or as All-items excluding the selections. Results are displayed in graphs and tables as percentage changes, index levels, or contributions to All-items percentage change.

## Installation

You can install the R package CPIAggr from GitHub using the following R code:
- pak::pak("CPICustomAggCalcAggSurMesureIPC/CPIAggr")

## Running the app in R
Once installed, you can run it using the following R code:
- in English: execute the code CPIAggr::CPIAggr("en"), or simply CPIAggr::CPIAggr()
- en français: executer CPIAggr::CPIAggr("fr")
- alternately, you can load the CPIAggr package into your R session via library("CPIAggr"), then run the code CPIAggr(), CPIAggr("en") or CPIAggr("fr") without the CPIAggr:: package specification

## Using the CPI Custom Aggregate Calculator
- English instructions: https://github.com/CPICustomAggCalcAggSurMesureIPC/CPIAggr
- Instructions en français: https://github.com/CPICustomAggCalcAggSurMesureIPC/CPIAggr

## Development:

- Gerry O'Donnell
- Principal Consumer Prices Analyst / Analyste principal des prix à la consommation
- Consumer Prices Division / Division des prix à la consommation
- Statistics Canada / Statistique Canada
- gerry.odonnell@statcan.gc.ca

## How it works:

- The package loads the file R\\App.R, which contains the CPIAggr <- function(fvcAppLanguage) which ...
    - Receives a language argument
	- Contains several internal-only functions
        - fPeriodSeq190001 converts a date as string ("yyyy-mm-dd") to a month in sequence starting 1900-01
        - fRefDate converts a month in sequence starting 1900-01 to date as string ("yyyy-mm-dd")
        - fRoundHAFZ uses fuzzy half-away-from-zero rounding at specified number of digits
        - fGetEnFrText retrieves English or French text for UI object
        - fGetVarNameFromEnFrText gets UI object name from English or French text
        - fIndexWeightChgCont accepts the selected series and base start and end periods, retrieves related CODR indexes and weights, calculates and returns CustAgg values and status message  
        - fGetDisplaySeries accepts component series, returns remaining available series
        - fPlotTimeSeries accepts dataframe and available series, returns plotly graphic
        - fMessage writes message to console by code block
    - Reads metadata in R\\data-raw\Data_for_R_Shiny.xlsx needed to initialize app with data specifying ...
        - Effective dates for CPI baskets
        - CODR table 18100004 and 18100007 series identifiers
        - Popular aggregate definitions and component series 
        - English and French text for UI components
	- Creates global variables
    - Defines reusable UI-related functions
    - Defines the ui function, which creates and positions UI objects and creates JS functions
    - Defines the server function, which receives user input, retrieves CODR data and displays results
    - Calls shinyApp(ui, server)





