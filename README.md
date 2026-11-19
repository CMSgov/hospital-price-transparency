[![CMS Transparency in Coverage](resources/images/HPT_banner.png?raw=true "Hospital Price Transparency")](https://www.cms.gov/priorities/key-initiatives/hospital-price-transparency)

# Hospital Price Transparency

The hospital price transparency requirements are codified in regulations at 45 CFR Part 180 and applies to facilities that meet the definition of hospital (defined at 45 CFR § 180.20) and that are not otherwise excepted (see 45 CFR § 180.30(b)). Hospitals must make their standard charge information publicly available in two ways:

1. A machine-readable file containing a list of all standard charges for all items and services as provided in § 180.50, and;
2. A consumer-friendly list of standard charges for a limited set of shoppable services as provided in § 180.60.

This repository provides resources for both requirements. Choose the section below that matches what you are preparing:

- **Machine-readable file (MRF)**: Find CSV and JSON data dictionaries, templates, examples, and tools to build and validate your machine-readable file.
- **Consumer-friendly display (CFD)**: Find a voluntary shoppable services sample file, completed example, data dictionary, and Consumer User Guide to help prepare your consumer-friendly display.

## Machine-readable File

To prepare your hospital’s machine-readable file:

1. Choose your file format: CSV or JSON.
2. Read the data dictionary for that format. It explains what information to include and how to enter it.
3. Create your file using the templates or schema and examples linked below.
4. Check your completed file using the MRF validator.

<table>
  <tr>
    <td width="154px"><a href="./Machine-readable file/documentation/CSV/"><img src="./resources/images/csv_start_here_button.png" /></a></td>
    <td>
      <h2>Developing a CSV MRF?</h2>
      <div>
        CSV files can use either a wide or tall layout. Review the CSV data dictionary for instructions on both layouts, then choose the matching template.
      </div>
      <div>
        <a href="./Machine-readable file/documentation/CSV/">Read the CSV data dictionary</a>
      </div>
    </td>
  </tr>
  <tr>
    <td colspan="2">Then build your file: <a href="./Machine-readable file/documentation/CSV/templates/V3.0.0_Tall_CSV_Format_Template.csv">CSV tall template</a> - <a href="./Machine-readable file/documentation/CSV/templates/V3.0.0_Wide_CSV_Format_Template.csv">CSV wide template</a> - <a href="./Machine-readable file/examples/CSV/">View examples</a></td>
  </tr>
</table>
<hr/>
<table>
  <tr>
    <td width="154px"><a href="./Machine-readable file/documentation/JSON/"><img src="./resources/images/json_start_here_button.png"/></a></td>
    <td>
      <h2>Developing a JSON MRF?</h2>
      <div>
        Review the JSON data dictionary for descriptions of each data element and instructions for completing your file.
      </div>
      <div>
        <a href="./Machine-readable file/documentation/JSON/">Read the JSON data dictionary</a>
      </div>
    </td>
  </tr>
  <tr>
    <td colspan="2">Then build your file: <a href="./Machine-readable file/documentation/JSON/schemas/">JSON schema and documentation</a> - <a href="./Machine-readable file/examples/JSON/">View examples</a></td>
  </tr>
</table>
<hr/>
<table>
  <tr>
    <td width="154px"><a href="https://cmsgov.github.io/hpt-tool/online-validator/"><img src="./resources/images/cloud_icon.png" /></a></td>
    <td>
      <h2>Ready to check your MRF?</h2>
      <div>
        Use the online validator to check your hospital's CSV or JSON file and identify errors to correct.
      </div>
      <div>
        <a href="https://cmsgov.github.io/hpt-tool/online-validator/">Open MRF validator</a>
      </div>
    </td>
  </tr>
  <tr>
    <td colspan="2">More MRF tools: Visit the <a href="https://cmsgov.github.io/hpt-tool/">Hospital Price Transparency tools page</a> for the <a href="https://cmsgov.github.io/hpt-tool/filename-wizard/">File Naming Wizard</a> and <a href="https://cmsgov.github.io/hpt-tool/txt-generator/">TXT File Generator</a>.</td> 
  </tr>
</table>
<hr/>

## Consumer-friendly Display

CMS developed the shoppable services voluntary sample file to help hospitals meet the consumer-friendly display requirements under 45 CFR § 180.60 of the Hospital Price Transparency regulations. The file provides a standardized format for displaying standard charges for shoppable services, reducing the burden of creating a display from scratch and helping consumers make meaningful comparisons across hospitals.

Developed with input from hospitals, consumers, and consumer tool developers, the shoppable services voluntary sample file is supported by a data dictionary, an example sample file, and a Consumer User Guide.

<table>
  <tr>
    <td width="154px"><a href="./Consumer-friendly display/"><img src="./resources/images/cfd_start_here.png"/></a></td>
    <td>
      <h2>Developing a consumer-friendly display?</h2>
      <div>
        The shoppable services data dictionary contains descriptions of each data element and instructions for completing the shoppable services voluntary sample file.
      </div>
      <div>
        <a href="./Consumer-friendly display/SHOPPABLE_SERVICES_VOLUNTARY_SAMPLE_FILE_DATA_DICTIONARY.pdf">Read the CFD data dictionary</a>
      </div>
    </td>
  </tr>
  <tr>
    <td colspan="2">Then prepare your display: <a href="./Consumer-friendly display/SS_Sample_Format.xlsx">Shoppable services voluntary sample file</a> - <a href="./Consumer-friendly display/SS_Sample_Format_Example_File.xlsx">Example sample file</a></td>
  </tr>
  <tr>
    <td colspan="2">Help consumers understand your display: <a href="./Consumer-friendly display/SHOPPABLE_SERVICES_VOLUNTARY_SAMPLE_FILE_CONSUMER_GUIDE.pdf">Consumer User Guide</a></td>
  </tr>
</table>

Use of the shoppable services voluntary sample file is optional. Hospitals that use it must include all data elements required by 45 CFR § 180.60(b).

## Resources and Support

Users should review the final rule(s) in their entirety as well as review any clarifying guidance provided on the [Hospital Price Transparency Resources](https://www.cms.gov/hospital-price-transparency/resources) webpage to ensure compliance.

- <a href="./resources/Navigating GitHub and the HPT Data Dictionary Guide.pdf/">Navigating GitHub Guide</a> - A step-by-step guide that walks users new to GitHub through the information and available resources on this HPT repository.
- [Github Issues](https://guides.github.com/features/issues/) - Where people discuss issues related to the project.
- [Github Discussions](https://github.com/CMSgov/hospital-price-transparency/discussions) - Use these channels for conversational topics (for example, "How do I&hellip;" or "What do you think about&hellip;" instead of bug reports or feature requests).
- [Hospital Price Transparency Tools](https://cmsgov.github.io/hpt-tool/) - Link to webpage of tools to support hospitals in meeting the accessibility and MRF requirements including a MRF File Naming Wizard, a TXT File Generator, and a Validator that tests against the required CMS template and data specifications.

Before posting a comment, issue, or question, please search through existing discussions and issues. There is a good chance that the topic in questions is already being discussed.

Policy questions can be directed to: PriceTransparencyHospitalCharges@cms.hhs.gov. Hospitals undergoing an enforcement action may direct questions to: HPTCompliance@cms.hhs.gov.
