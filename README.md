# Data360 OpenAPI Specifications

OpenAPI specifications for the World Bank's [Data360](https://data360.worldbank.org) APIs. The public Data360 specification in this repository powers the [Data360 API documentation page](https://data360.worldbank.org/en/api#/).

## Specifications

| File | API | Server | OpenAPI | Status |
|------|-----|--------|---------|--------|
| [`Data360 Open_API.json`](Data360%20Open_API.json) | Data360 API (public) | `https://data360api.worldbank.org` | 3.0.1 | **Published**: feeds the [Data360 API documentation page](https://data360.worldbank.org/en/api#/) |
| [`findi-open-api.json`](findi-open-api.json) | FINDI API | `https://data360api.worldbank.org` | 3.0.1 | **Draft**: under review, not yet published |
| [`data360-int-open-api.json`](data360-int-open-api.json) | Data360 internal API | `https://datacatalogapiqa.worldbank.org` (QA) | 3.0.3 | **Draft**: internal use only |
| [`archives/`](archives/) | Earlier versions of the Data360 specification | | | Historical reference, not maintained |

> [!IMPORTANT]
> Changes to `Data360 Open_API.json` that are merged into `main` update the live Data360 API documentation page. Do not rename or move this file: the documentation page depends on its path.

### Data360 API

Public API for searching Data360 and retrieving data and metadata. No authentication is required.

| Method | Path | Description |
|--------|------|-------------|
| GET | `/data360/data` | Data based on provided filters |
| GET | `/data360/disaggregation` | Disaggregations for a given indicator |
| GET | `/data360/indicators` | List of indicator IDs |
| POST | `/data360/metadata` | Metadata based on provided filters |
| POST | `/data360/searchv2` | Search Data360 |

### FINDI API (draft)

Data and metadata for FINDI datasets hosted on the Data360 platform.

| Method | Path | Description |
|--------|------|-------------|
| GET | `/data360/data` | Data based on provided filters |
| GET | `/data360/portal/v1/data` | Indicator data based on provided filters |
| POST | `/data360/portal/v1/temporaldata` | Indicator time series data |
| POST | `/data360/portal/v1/dimensions` | Disaggregations for a given indicator |
| GET | `/data360/portal/v1/hierarchy` | Hierarchy |
| GET | `/data360/portal/v1/metadata` | Dataset or indicator metadata |
| POST | `/data360/portal/v1/get_entities_by_id` | Entities by ID, with specified fields |
| POST | `/data360/portal/v1/entities_by_economy_topic_tag` | Entities by economy, topic, and tags, with pagination |

Still to document: the `/dimensions` request body (`DimensionDataDetails`), the `/hierarchy` parameters, and the response schemas of the non-data endpoints.

### Data360 internal API (draft)

Internal API on the QA environment. Requests need an API Management subscription key (`Ocp-Apim-Subscription-Key` header) and a bearer token (JWT).

| Method | Path | Description |
|--------|------|-------------|
| POST | `/data/int/v3/data360/search` | Search for indicators and datasets |
| GET | `/data/int/v3/data360/data` | Query Data360 observations |
| GET | `/data/int/v3/data360/disaggregation` | Available disaggregations for an indicator in a dataset |
| GET | `/data/int/v3/data360/codelist` | Codelist metadata and codes |
| GET | `/data/int/v3/data360/getuseraction` | User action statistics |
| POST | `/data/int/v3/data360/saveuseraction` | Save a user action |

## Viewing a specification

- **In the browser:** open the [Swagger Editor](https://editor.swagger.io) and paste in the file contents.
- **In VS Code:** install an OpenAPI extension and open the file to get a rendered preview.

## Validating a specification

Validate a specification before opening a pull request:

```bash
pip install openapi-spec-validator
python -m openapi_spec_validator findi-open-api.json
```

A valid file prints `<file>: OK`. Put file names that contain spaces in quotes, for example `python -m openapi_spec_validator "Data360 Open_API.json"`.

## Contributing

1. Create a branch from `main` with a descriptive prefix: `docs/` for documentation changes, `fix/` for corrections, `feature/` for new endpoints, `chore/` for maintenance. For example: `docs/findi-hierarchy-params`.
2. Edit the specification. Keep the 2-space JSON indentation and give every operation a unique `operationId`.
3. Validate the file (see [Validating a specification](#validating-a-specification)).
4. Open a pull request against `main` in [worldbank/open-api-specs](https://github.com/worldbank/open-api-specs) and get at least one review before merging.

## Support

- Questions about the APIs or the data: data@worldbank.org
- Problems with the specifications in this repository: [open an issue](https://github.com/worldbank/open-api-specs/issues)

## License

The contents of this repository are licensed under the [MIT License](LICENSE) with the [World Bank IGO Rider](WB-IGO-RIDER.md). The public specifications declare the [Creative Commons Attribution 4.0 (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/) license for the APIs they describe.
