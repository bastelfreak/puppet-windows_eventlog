# puppet-windows_eventlog

#### Table of Contents

1. [Overview](#overview)
2. [Module Description - What is the windows_eventlog module?](#module-description)
3. [Setup - The basics of getting started with windows_eventlog](#setup)
    * [What windows_eventloge affects](#what-windows_eventlog-affects)
    * [Setup requirements](#setup-requirements)
    * [Beginning with windows_eventlog](#beginning-with-windows_eventlog)
4. [Usage - Configuration options and additional functionality](#usage)
5. [Reference - An under-the-hood peek at what the module is doing and how](#reference)
5. [Limitations - OS compatibility, etc.](#limitations)
6. [Development - Guide for contributing to the module](#development)

## Overview

Puppet module for managing windows event logs

[![Build Status](https://travis-ci.org/voxpupuli/puppet-windows_eventlog.svg?branch=master)](https://travis-ci.org/voxpupuli/puppet-windows_eventlog)

## Module Description

The purpose of this module is to manage each of the Windows event logs, including the size, rotation and retention

## Setup

### What windows_eventlog affects

* Sets registry keys to manage the event log configuration

### Beginning with windows_eventlog

  Manage the size of the Application log:

```puppet
    windows_eventlog { 'Application':
      log_path => '%SystemRoot%\system32\winevt\Logs\Application.evtx',
      log_size => '2048',
      max_log_policy => 'overwrite'
    }
```

  Manage several custom logs under C:\Logs:

```puppet
   windows_eventlog { ['Custom1', 'Custom2', 'Custom3']:
     log_path_template => 'C:\Logs\%%NAME%%.evtx'
   }
```

## Usage

### Classes and Defined Types:

#### Defined Type: `windows_eventlog`

The primary definition of this module. Manages the size and rotation policy of Windows event logs

**Parameters within `windows_eventlog`:**
##### `log_path`

_(Optional)_ The path to the log file that you want to manage.

##### `log_size`

The max size of the log file.  Defaults to '`1028`'.

##### `max_log_policy`

The retention policy for the log.  Defaults to '`overwrite`'.

##### `log_path_template`

_(Optional)_ A template for `log_path`, where "`%%NAME%%`" will be replaced with the log name.  Defaults to '`%SystemRoot%\\system32\\winevt\\Logs\\%%NAME%%.evtx`'.

## Reference

### Defined Types

### Public Defined Types

* [`windows_eventlog`](#define-eventlog): Manages the size and rotation policy of a Windows event log

## Limitations

This module is tested on the following platforms:

* Windows 2008 R2

It is tested with the OSS version of Puppet only.

## Development

### Contributing

Please read CONTRIBUTING.md for full details on contributing to this project.
