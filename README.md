# Tax Calculator 
The Tax Calculator customization is a custom javascript plugin that runs with a default BBIS donation form. 

![Tax Calculator image](https://raw.githubusercontent.com/LindaBrennan/UWT-Tax-Calculator/master/taxCalculator.png "Calculator")

##About the Customization

The Tax Calculator customization is driven from management parameter that allows the BBIS administrator to provide the federal tax and provincial tax rates as arguments. This will allow the customization calculation to be updated each year the tax rates change. The language options will also be passed in as arguments too.

### Library
A library of messages and range values for use with Tax Calculator must be used with the custom script. Said library is a JSON object stored in a text file. A text file is used to make uploading to the BBIS Document Part a simple task. 

Each item or object in the library requires a message, rangeMax, rangeMin. All range values (rangeMax and rangeMin) must be a floating point integer.

#### Libray JSON Example
    [
		{
			"message": "A message where the range min is 0.00 and range max is 99.99",
			"rangeMax" : 99.99,
			"rangeMin" : 0.00
		},
		{
			"message": "A message where the range min is 100.00 and range max is 499.99",
			"rangeMax" : 499.00,
			"rangeMin" : 100.00
		},
		{
			"message": "A message where the range min is 500.00 and range max is 999.99",
			"rangeMax" : 999.99,
			"rangeMin" : 500.00
		},
		{
			"message": "A message where the range min is 1000.00 and range max is 1000000000000",
			"rangeMax" : 1000000000000,
			"rangeMin" : 1000.00
		}
    ]


##Setup
### Library
The location of said library in the BBIS Documents part must be provided as an argument to the custom script at runtime. The user must upload the the JSON file to the BBIS Documents part. Once the file is uploaded, the file location must be passed.

*    Upload the “taxCalculatorLibrary.txt” to a BBIS Document Part
*    Make note of the URL
*    Provide the URL to the script as an argument at runtime 

	jQuery('document').ready( function(){
		filelocation = {
			bbisDocumentURL : 'taxCalculatorLibrary.txt'
		});
	});

### Tax Tip
The script must know the tax rates to calculate the total cost of the gift and display the dollar amount. The user must provide the Federal Max, Federal Min, Providence Max, Providence Min and Gift Ceiling as argument at runtime.  


jQuery('document').ready( function(){
	taxrate = {
		Fed_max : 29.00,
		Fed_min : 15.00,
		Prov_max : 11.16,
		Prov_min : 5.05,
		Gift_ceil : 200.00
	}); 

### Page Configuration
To install the customization into a BBIS page a user must add one (1) Unformatted Text and Images Part to a BBIS page. The Page must also contain one (1) BBIS Donation Form. 

*    Create one (1) new Unformatted Text and Image Part 
*    Add the following to said part
	<!--The tax tip calculator js -->
	<script type="text/javascript" src="taxCalculator.js"></script>
	<!-- html element to be placed onto the page with a donation form -->
	<div id="taxCalculator"></div>
	<script>
	jQuery('document').ready( function(){
	// expected arguments are Federal Tax Rate + Provincial Tax Rate
		taxCalculator.init(taxrate = {
			Fed_max : 29.00,
			Fed_min : 15.00,
			Prov_max : 11.16,
			Prov_min : 5.05,
			Gift_ceil : 200.00
		},
		filelocation = {
			bbisDocumentURL : 'taxCalculatorLibrary.txt'
		});
	});
	</script>
*    Add the part to a BBIS page in conjunction with a BBIS Donation Form

##Assumptions
*    United Way Toronto will be responsible for providing and managing tax statements and corresponding range values
*    United Way Toronto will be responsible for providing and managing  federal tax and provincial tax rates.
*    Text associated with each impact statement should be free text. We should avoid embedding text into our images