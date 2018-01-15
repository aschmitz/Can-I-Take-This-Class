Can I Take This Class offers a prediction API to enable other applications to build on its data. The format of the API is outlined below.

# API Reference

## URL

[https://canitakethisclass.com/api](https://canitakethisclass.com/api)

## Format

JSON

## Types
* `Course`: A string containing a 2-4 character subject code (case insensitive) followed by a 3-digit course number.
* `Date`: A string in the format "YYYY-MM-DD".
* `Chance`: An object containing two floats in the range [0, 1]: `percent`, the likelihood of an event; and `error`, the standard error of the likelihood.
* `Prediction`: An object containing two Chances: `on_date`, the likelihood of being able to register on the given date; and `after_date`, the likelihood of being able to register after the given date.

## Parameters
* `String courses`: A comma-separated list of Courses.
* `Date date`: The registration date.

## Result
* `String error`: If an error occurred, contains a description of the error. Will not exist if an error did not occur.
* `Prediction overall`: The likelihood of getting into all of the requested courses.
* `Object courses`: An object containing, for each requested course:
    - `Prediction overall`: The likelihood of getting into the course.
    - `Object sections`: An object containing the Prediction for each section in the course.

## Example

### Request URL

[https://canitakethisclass.com/api?courses=cs225,cs233&date=2016-04-11](https://canitakethisclass.com/api?courses=cs225,cs233&date=2016-04-11)

### Response

Formatted for clarity. The actual response is minified.

    {
      "overall": {
        "on_date": {
          "percent": 0.9643,
          "error": 0.034408792480992
        },
        "after_date": {
          "percent": 0.25875,
          "error": 0.02229142148461
        }
      },
      "courses": {
        "cs225": {
          "overall": {
            "on_date": {
              "percent": 0.9643,
              "error": 0.034408792480992
            },
            "after_date": {
              "percent": 0.25875,
              "error": 0.02229142148461
            }
          },
          "sections": {
            "Laboratory-Discussion": {
              "on_date": {
                "percent": 0.9647,
                "error": 0.011427165922999
              },
              "after_date": {
                "percent": 0.5779,
                "error": 0.0088835322571266
              }
            },
            "Lecture": {
              "on_date": {
                "percent": 0.9643,
                "error": 0.034408792480992
              },
              "after_date": {
                "percent": 0.25875,
                "error": 0.02229142148461
              }
            }
          }
        },
        "cs233": {
          "overall": {
            "on_date": {
              "percent": 1,
              "error": 0
            },
            "after_date": {
              "percent": 0.58585,
              "error": 0.028675014339463
            }
          },
          "sections": {
            "Discussion\/Recitation": {
              "on_date": {
                "percent": 1,
                "error": 0
              },
              "after_date": {
                "percent": 0.6792,
                "error": 0.010438972608586
              }
            },
            "Lecture": {
              "on_date": {
                "percent": 1,
                "error": 0
              },
              "after_date": {
                "percent": 0.58585,
                "error": 0.028675014339463
              }
            }
          }
        }
      }
    }
