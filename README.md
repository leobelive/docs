# Project Geode End-User Documentation

Project Geode provides the full source for end-user documentation in DITA XML format. The DITA XML can be built into HTML or PDF output using [Bookbinder](https://github.com/cloudfoundry-incubator/bookbinder).  

Bookbinder is a gem that binds together a unified documentation web application from markdown, html, and/or DITA source material. The source material for bookbinder must be stored either in local directories or in GitHub repositories. Bookbinder runs [middleman](http://middlemanapp.com/) to produce a Rackup app that can be deployed locally or as a Web application.

## Usage

Bookbinder is meant to be used from within a project called a **book**. The book includes a configuration file that describes which documentation repositories to use as source materials. Bookbinder provides a set of scripts to aggregate those repositories and publish them to various locations.

For project Geode, a preconfigured **book** is provided in the directory `/geode-book`.  You can use this configuration to build HTML for project Geode on your local system.

## Prerequisites

* Bookbinder requires Ruby version 2.0.0-p195 or higher.
* Building DITA documentation in bookbinder requires:
  * Java 1.7
  * Ant
  * The [DITA Open Toolkit (DITA-OT) 1.7.5](http://sourceforge.net/projects/dita-ot/files/DITA-OT%20Stable%20Release/DITA%20Open%20Toolkit%201.7/)

## Procedure

To begin, move or copy the `/geode-book directory` to a directory that is parallel to `project-geode/docs`. For example:

    $ cd /repos/project-geode/docs
    $ mv geode-book ..
    $ cd ../geode-book

The GemFile in the book directory already defines the `gem "bookbindery"` dependency. Make sure you are in the relocated book directory and enter:

    $ bundle install
     
The installed `config.yml` file configures the Project Geode book for building locally.  The installed file configures the local directory for the DITA source files, and identifies the main DITA map file to build. It contains:

    book_repo: Pivotal-DataFabric/docs-book-geode
    dita_sections:
    - repository:
        name: project-geode/docs
      directory: docs
      ditamap_location: Geode.ditamap
   
    template_variables:
      support_url: https://github.com/project-geode/docs
      product_url: https://github.com/project-geode
      book_title: Project Geode Documentation

To build the files locally using the installed `config.yml` file, execute:

    $ bundle exec bookbinder bind local
    
Bookbinder converts the XML source into HTML, putting the final output in the `final_app` directory.  To view the local documentation:

    $ cd final_app
    $ rackup
    
You can now view the local documentation at [http://localhost:9292](http://localhost:9292)

### Getting More Information

Bookbinder provides additional functionality to construct books from multiple Github repos, to perform variable substitution, and also to automatically build documentation in a continuous integration pipeline.  For more information, see [https://github.com/cloudfoundry-incubator/bookbinder](https://github.com/cloudfoundry-incubator/bookbinder).
