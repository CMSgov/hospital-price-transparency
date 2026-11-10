# Hospital Price Transparency

The hospital price transparency requirements are codified in regulations at 45 CFR Part 180 and applies to facilities that meet the definition of hospital (defined at 45 CFR § 180.20) and that are not otherwise excepted (see 45 CFR § 180.30(b)). Hospitals must make their standard charge information publicly available in two ways:

1. A machine-readable file containing a list of all standard charges for all items and services as provided in § 180.50, and;
2. A consumer-friendly list of standard charges for a limited set of shoppable services as provided in § 180.60.

This repository provides resources for both requirements. Choose the section below that matches what you are preparing:

- **Machine-readable file**: Find CSV and JSON data dictionaries, templates, examples, and tools to build and validate your machine-readable file.

[Machine-readable File](#machine-readable-file) · [Resources and Support](#resources-and-support)

## Machine-readable File

To prepare your hospital’s machine-readable file:

1. Choose your file format: CSV or JSON.
2. Read the data dictionary for that format. It explains what information to include and how to enter it.
3. Create your file using the templates or schema and examples linked below.
4. Check your completed file using the MRF validator.

<table>
  <tr>
    <td width="154px"><img src="./resources/images/start_here.png" /></td>
    <td>
      <h2>Developing a CSV MRF?</h2>
      <div>
        CSV files can use either a wide or tall layout. Review the CSV data dictionary for instructions on both layouts, then choose the matching template.
      </div>
      <div>
        <a href="./MRF/documentation/CSV/">Read the CSV data dictionary</a>
      </div>
    </td>
  </tr>
  <tr>
    <td colspan="2">Then build your file: <a href="./MRF/documentation/CSV/templates/V3.0.0_Tall_CSV_Format_Template.csv">CSV tall template</a> - <a href="./MRF/documentation/CSV/templates/V3.0.0_Wide_CSV_Format_Template.csv">CSV wide template</a> - <a href="./MRF/examples/CSV/">View examples</a></td>
  </tr>
</table>
<hr/>
<table>
  <tr>
    <td width="154px"><img src="./resources/images/start_here.png" /></td>
    <td>
      <h2>Developing a JSON MRF?</h2>
      <div>
        Review the JSON data dictionary for descriptions of each data element and instructions for completing your file.
      </div>
      <div>
        <a href="./MRF/documentation/JSON/">Read the JSON data dictionary</a>
      </div>
    </td>
  </tr>
  <tr>
    <td colspan="2">Then build your file: <a href="./MRF/documentation/JSON/schemas/">JSON schema and documentation</a> - <a href="./MRF/examples/JSON/">View examples</a></td>
  </tr>
</table>
<hr/>
<table>
  <tr>
    <td width="154px"><img src="./resources/images/cloud_icon.png" /></td>
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
    <td colspan="2">More MRF tools: <a href="https://cmsgov.github.io/hpt-tool/">File naming wizard and TXT file generator</a></td>
  </tr>
</table>
<hr/>

## Resources and Support

Users should review the final rule(s) in their entirety as well as review any clarifying guidance provided on the Hospital Price Transparency Resources webpage to ensure compliance.

- Navigating GitHub Guide – A step-by-step guide that walks users new to GitHub through the information and available resources on this HPT repository.
- Github Issues - Where people discuss issues related to the project.
- Github Discussions - Use these channels for conversational topics (for example, "How do I…" or "What do you think about…" instead of bug reports or feature requests).
- Hospital Price Transparency Tools - Link to webpage of tools to support hospitals in meeting the accessibility and MRF requirements including a MRF File Naming Wizard, a TXT File Generator, and a Validator that tests against the required CMS template and data specifications.

Before posting a comment, issue, or question, please search through existing discussions and issues. There is a good chance that the topic in questions is already being discussed. Policy questions can be directed to: PriceTransparencyHospitalCharges@cms.hhs.gov. Hospitals undergoing an enforcement action may direct questions to: HPTCompliance@cms.hhs.gov.
