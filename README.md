zipcode-mexico
zipcode-mexico is a REST API that maps all the data from the current zip codes in Mexico. You can get the CSV or Excel files from the official site

We build this API in order to provide a way to developers query the zip codes, states and municipalities across the country.

Table of contents
Quick start
Querying the API
About pagination
Development
Setup the project
Running the project
Stop the project
Running specs
Contributing
License
Quick start
The base URI to start consuming the JSON response is under:

http://sepomex.icalialabs.com/api/v1/zip_codes
There are currently 145,481 records on the database which were extracted from the CSV file included in the project.

Records are paginated with 15 records per page.

Running the project
Pending. Here will be the instructions to run the project with Docker. TBD

Querying the API
We currently provide 4 kind of resources:

Zip Codes: http://sepomex.icalialabs.com/zip_codes
States: http://sepomex.icalialabs.com/states
Municipalities: http://sepomex.icalialabs.com/municipalities
Cities: http://sepomex.icalialabs.com/cities
ZipCodes
In order to provide more flexibility to search a zip code, whether is by city, colony, state or zip code you can now send multiple parameters to make the appropiate search. You can fetch the:

all
curl -X GET https://sepomex.icalialabs.com/api/v1/zip_codes 
Response
{
  "zip_codes": [
    {
      "id": 1,
      "d_codigo": "01000",
      "d_asenta": "San Ángel",
      "d_tipo_asenta": "Colonia",
      "d_mnpio": "Álvaro Obregón",
      "d_estado": "Ciudad de México",
      "d_ciudad": "Ciudad de México",
      "d_cp": "01001",
      "c_estado": "09",
      "c_oficina": "01001",
      "c_cp": null,
      "c_tipo_asenta": "09",
      "c_mnpio": "010",
      "id_asenta_cpcons": "0001",
      "d_zona": "Urbano",
      "c_cve_ciudad": "01"
    },
    ... 
  ],
  "meta": {
    "pagination": {
      "per_page": 15,
      "total_pages": 9728,
      "total_objects": 145906,
      "links": {
        "first": "/zip_code?page=1",
        "last": "/zip_code?page=9728",
        "next": "/zip_code?page=2"
      }
    }
  }
}
by city
curl -X GET https://sepomex.icalialabs.com/api/v1/zip_codes?city=monterrey
by state
curl -X GET https://sepomex.icalialabs.com/api/v1/zip_codes?state=nuevo%20leon
by colony
curl -X GET https://sepomex.icalialabs.com/api/v1/zip_codes?colony=punta%20contry
by cp
curl -X GET https://sepomex.icalialabs.com/api/v1/zip_codes?zip_code=67173
all together
curl -X GET https://sepomex.icalialabs.com/api/v1/zip_codes?colony=punta%20contry&state=nuevo%20leon&city=guadalupe
States
The states resources can be fetch through several means:

all
curl -X GET https://sepomex.icalialabs.com/api/v1/states
Response
{
  
  "states": [
    {
      "id": 1,
      "name": "Ciudad de México",
      "cities_count": 16
    },
    ...
  ],
  "meta": {
    "pagination": {
      "per_page": 15,
      "total_pages": 3,
      "total_objects": 32,
      "links": {
        "first": "/state?page=1",
        "last": "/state?page=3",
        "next": "/state?page=2"
      }
    }
  }
}
by id
curl -X GET https://sepomex.icalialabs.com/api/v1/states/1
Response
{
  "state": {
    "id": 1,
    "name": "Ciudad de México",
    "cities_count": 16
  }
}
states municipalities
curl -X GET https://sepomex.icalialabs.com/api/v1/states/1/municipalities
Response
{
  "municipalities": [
    {
      "id": 1,
      "name": "Álvaro Obregón",
      "municipality_key": "010",
      "zip_code": "01001",
      "state_id": 1
    },
    ...
    {
      "id": 16,
      "name": "Xochimilco",
      "municipality_key": "013",
      "zip_code": "16001",
      "state_id": 1
    }
  ]
}
Municipalities
all
curl -X GET https://sepomex.icalialabs.com/api/v1/municipalities
Response
{
  "municipalities": [
    {
      "id": 1,
      "name": "Álvaro Obregón",
      "municipality_key": "010",
      "zip_code": "01001",
      "state_id": 1
    },
    ...
  ],
  "meta": {
    "pagination": {
      "per_page": 15,
      "total_pages": 155,
      "total_objects": 2318,
      "links": {
        "first": "/municipality?page=1",
        "last": "/municipality?page=155",
        "next": "/municipality?page=2"
      }
    }
  }
}
by id
curl -X GET https://sepomex.icalialabs.com/api/v1/municipalities/1
Response
{
  "municipality": {
    "id": 1,
    "name": "Álvaro Obregón",
    "municipality_key": "010",
    "zip_code": "01001",
    "state_id": 1
  }
}
Cities
all
curl -X GET https://sepomex.icalialabs.com/api/v1/cities
Response
{
  "cities": [
    {
      "id": 1,
      "name": "Ciudad de México",
      "state_id": 1
    },
  ...
  ],
  "meta": {
    "pagination": {
      "per_page": 15,
      "total_pages": 45,
      "total_objects": 669,
      "links": {
        "first": "/city?page=1",
        "last": "/city?page=45",
        "next": "/city?page=2"
      }
    }
  }
}
by id
curl -X GET https://sepomex.icalialabs.com/api/v1/cities/1
Response
{
  "city": {
    "id": 1,
    "name": "Ciudad de México",
    "state_id": 1
  }
}
About pagination
The structure of a paged response is:

"meta": {
    "pagination": {
      "per_page": 15,
      "total_pages": 9728,
      "total_objects": 145906,
      "links": {
        "first": "/zip_code?page=1",
        "last": "/zip_code?page=9728",
        "prev": "/zip_code?page=1",
        "next": "/zip_code?page=3"
      }
    }
  }
Where:

per_page is the amount of elements per page.
total_pages is the total number of pages.
total_objects is the total objects of all pages.
links contains links for pages.
firstis the url for the first page.
last is the url for the last page.
prev is the url for the previous page.
next is the url for the next page.
Development
Setup the project

To setup the project please follow this simple steps:

Clone this repository into your local machine:
$ git clone git@github.com:IcaliaLabs/sepomex.git
Change directory into the project folder:
$ cd sepomex
Run the web service in bash mode to get inside the container by using the following command:
$ docker-compose run web bash
Inside the container you need to migrate the database:
$ rails db:migrate
Next you should populate the database:
$ rails db:seed
This operation will take some time, due to the number of records.

Close the container
$ exit
Running the project

Fire up a terminal and run:
$ docker-compose up
Once you see an output like this:

web_1        | The Gemfile's dependencies are satisfied
web_1        | 2020/08/04 17:40:21 Waiting for: tcp://postgres:5432
web_1        | 2020/08/04 17:40:21 Connected to tcp://postgres:5432
web_1        | => Booting Puma
web_1        | => Rails 6.0.3.2 application starting in development 
web_1        | => Run `rails server --help` for more startup options
web_1        | Puma starting in single mode...
web_1        | * Version 3.12.6 (ruby 2.7.1-p83), codename: Llamas in Pajamas
web_1        | * Min threads: 5, max threads: 5
web_1        | * Environment: development
web_1        | * Listening on tcp://0.0.0.0:3000
web_1        | Use Ctrl-C to stop
This means the project is up and running.

Stop the project

Use Ctrl-C to stop.

If you want to remove the containers use:

$ docker-compose down
Running specs

To run specs, you can do:

$ docker-compose run test rspec
Contributing
Please submit all pull requests against a separate branch.

