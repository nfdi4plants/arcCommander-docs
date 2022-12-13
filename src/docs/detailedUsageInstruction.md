---
layout: docs
title: Metadata
date: 2022-12-13
add toc: true
add sidebar: _sidebars/mainSidebar.md
Article Status: Publishable
---


### General cli structure

The general command line structure is designed as either

```powershell
arc <top-level-command> <top-level-command-args>
```

e.g.

```powershell
arc init
```

or

```powershell
arc <object> <subcommand-verb> <subcommand-verb-args>
```

where `<object>` is one of the following:

 - `assay` 
 - `study`  or its sub-objects 
 - `investigation` or its sub-objects 
 - `configuration`

and `<subcommand-verb>` models what to do with the object, e.g

```powershell
arc study init
```

will initialize a new empty study in the ARC.

### Subcommand verbs

while not all object subcommands support all verbs, here is a list of the verbs and what to expect when they are applicable for an `<object>`:

- arc `<object>` **init** : will initialize a new empty `<object>` in the ARC.
- arc `<object>` **create** will create a new `<object>` with the passed arguments in the ARC.
- arc `<object>` **update** will update the registration of an existing `<object>` with the passed arguments.
- arc `<object>` **edit** will open an existing `<object>` with a text editor, allowing editing the registration of the `<object>`. 
- arc `<object>` **register** will register an existing `<object>` in the ARC with the passed arguments.
- arc `<object>` **add** is the combination of create/init+update and register, meaning it will create a new `<object>` in the ARC and subsequently register it with the passed arguments
- arc `<object>` **delete** will delete the `<object>` from the arc file structure.
- arc `<object>` **unregister** will remove the `<object>` from the ARC's register.
- arc `<object>` **remove** is the combination of delete and unregister, meaning it will delete the `<object>` from the ARC file structure and the ARC's registry
- arc `<object>` **move** will move the `<object>` from source to target register.
- arc `<object>` **list** will print all `<object>s` registered in the ARC.
- arc `<object>` **set** will set a single value in the `<object>`.
- arc `<object>` **unset** will remove a single value from the `<object>`.

### CLI argument help

Here is the current help dump from the command line tool:

#### Top level:

```powershell
USAGE: arc [--help] [--workingdir <working directory>] [--verbosity <verbosity>]
                        [<subcommand> [<options>]]

SUBCOMMANDS:

    init <init args>      Initializes basic folder structure
    investigation, i <verb and args>
                          Investigation file functions
    study, s <verb and args>
                          Study functions
    assay, a <verb and args>
                          Assay functions
    configuration, config <verb and args>
                          Configuration editing

    Use 'arc <subcommand> --help' for additional information.

OPTIONS:

    --workingdir, -p <working directory>
                          Set the base directory of your ARC
    --verbosity, -v <verbosity>
                          Sets the amount of additional printed information: 0->No information, 1 (Default) -> Basic
                          Information, 2 -> Additional information
    --help                display this list of options.
```

#### init: 

```powershell
USAGE: arc init [--help] [--owner <owner>] [--repositoryadress <repository adress>] [--editorpath <editor path>]

OPTIONS:

    --owner <owner>       Owner of the arc
    --repositoryadress <repository adress>
                          Github adress
    --editorpath <editor path>
                          The path leading to the editor used for text prompts (Default in Windows is notepad)
    --help                display this list of options.
```
<br>

#### investigation:

```powershell
USAGE: arc.exe investigation [--help] [<subcommand> [<options>]]

SUBCOMMANDS:

    create <create args>  Create a new investigation with the given Metadata
    update <update args>  Update the ARC's investigation with the given Metdadata
    edit                  Open an editor window to directly edit the ARC's investigation file
    delete <delete args>  Delete the ARC's investigation file (DANGER ZONE!)
    person <person verbs> Person functions
    publication <publication verbs>
                          Publication functions
    show                  Get the values of the ARC's investigation

    Use 'arc.exe <subcommand> --help' for additional information.

OPTIONS:

    --help                display this list of options.

OPTIONS:

    --help                display this list of options.
```

##### investigation create

```powershell
USAGE: arc investigation create [--help] --identifier <investigation identifier> [--title <title>]
                                             [--description <description>] [--submissiondate <submission date>]
                                             [--publicreleasedate <public release date>]

OPTIONS:

    --identifier <investigation identifier>
                          A identifier or an accession number provided by a repository. This SHOULD be locally unique.
    --title <title>       A concise name given to the investigation.
    --description <description>
                          A textual description of the investigation.
    --submissiondate <submission date>
                          The date on which the investigation was reported to the repository.
    --publicreleasedate <public release date>
                          The date on which the investigation was released publicly.
    --help                display this list of options.
```

##### investigation update

Give new metadata that overwrite the current metadata of an investigation.

```powershell
USAGE: arc investigation update [--help] --identifier <investigation identifier> [--title <title>]
                                             [--description <description>] [--submissiondate <submission date>]
                                             [--publicreleasedate <public release date>]

OPTIONS:

    --identifier <investigation identifier>
                          A identifier or an accession number provided by a repository. This SHOULD be locally unique.
    --title <title>       A concise name given to the investigation.
    --description <description>
                          A textual description of the investigation.
    --submissiondate <submission date>
                          The date on which the investigation was reported to the repository.
    --publicreleasedate <public release date>
                          The date on which the investigation was released publicly.
    --help                display this list of options.
```

##### investigation edit

Take the current metadata of an investigation and change it.  
(While `investigation edit` opens the current metadata that can be altered by the user, `investigation update` will take a new set of metadata and overwrites the existing one)

```powershell
USAGE: arc investigation edit [--help]

OPTIONS:

    --identifier <study identifier>
                          A unique identifier, either a temporary identifier supplied by users or one generated by a
                          repository or other database. For example, it could be an identifier complying with the LSID
                          specification.
    --help                display this list of options.

```

##### investigation delete

```powershell
USAGE: arc investigation delete [--help] --identifier <investigation identifier>

OPTIONS:

    --identifier <investigation identifier>
                          DangerZone: In order to delete this investigation file please provide its identifier here.
    --help                display this list of options.
```

<br>


##### investigation person

```powershell
USAGE: arc investigation person [--help] [<subcommand> [<options>]]

SUBCOMMANDS:

    update <update args>  Update an existing person in the arc investigation with the given person metadata. The person is
                          identified by the full name (first name, last name, mid initials)
    edit <edit args>      Open and edit an existing person in the arc investigation with a text editor. The person is
                          identified by the full name (first name, last name, mid initials)
    register <register args>
                          Register a person in the arc investigation with the given assay metadata.
    unregister <remove args>
                          Unregister a person from the given investigation. The person is identified by the full name (first
                          name, last name, mid initials).
    show <show args>      Show the metadata of a person registered in the arc investigation
    list                  List all persons registered in the arc investigation

    Use 'arc <subcommand> --help' for additional information.

OPTIONS:

    --help                display this list of options.
```

##### investigation person update

```powershell
OPTIONS:

    --lastname, -l <last name>
                          The last name of a person associated with the investigation.
    --firstname, -f <first name>
                          The first name of a person associated with the investigation.
    --midinitials, -m <mid initials>
                          The middle initials of a person associated with the investigation.
    --email <e mail>      The email address of a person associated with the investigation.
    --phone <phone number>
                          The telephone number of a person associated with the investigation.
    --fax <fax number>    The fax number of a person associated with the investigation.
    --address <adress>    The address of a person associated with the investigation.
    --affiliation <affiliation>
                          The organization affiliation for a person associated with the investigation.
    --roles <roles>       Term to classify the role(s) performed by this person in the context of the investigation, which
                          means that the roles reported here need not correspond to roles held withing their affiliated
                          organization. Multiple annotations or values attached to one person can be provided by using a
                          semicolon (";") Unicode (U0003+B) as a separator (e.g.: submitter;funder;sponsor). The term can be
                          free text or from, for example, a controlled vocabulary or an ontology. If the latter source is used
                          the Term Accession Number and Term Source REF fields below are required.
    --rolestermaccessionnumber <roles term accession number>
                          The accession number from the Term Source associated with the selected term.
    --rolestermsourceref <roles term source ref>
                          dentifies the controlled vocabulary or ontology that this term comes from. The Source REF has to
                          match one of the Term Source Names declared in the Ontology Source Reference section.
    --help                display this list of options.
```


##### investigation person edit

```powershell
USAGE: arc investigation person edit [--help] --lastname <last name> --firstname <first name>
                                                  [--midinitials <mid initials>]

OPTIONS:

    --lastname, -l <last name>
                          The last name of a person associated with the investigation.
    --firstname, -f <first name>
                          The first name of a person associated with the investigation.
    --midinitials, -m <mid initials>
                          The middle initials of a person associated with the investigation.
    --help                display this list of options.
```


##### investigation person register

```powershell
USAGE: arc investigation person register [--help] --lastname <last name> --firstname <first name>
                                                      [--midinitials <mid initials>] [--email <e mail>]
                                                      [--phone <phone number>] [--fax <fax number>] [--address <adress>]
                                                      [--affiliation <affiliation>] [--roles <roles>]
                                                      [--rolestermaccessionnumber <roles term accession number>]
                                                      [--rolestermsourceref <roles term source ref>]

OPTIONS:

    --lastname, -l <last name>
                          The last name of a person associated with the investigation.
    --firstname, -f <first name>
                          The first name of a person associated with the investigation.
    --midinitials, -m <mid initials>
                          The middle initials of a person associated with the investigation.
    --email <e mail>      The email address of a person associated with the investigation.
    --phone <phone number>
                          The telephone number of a person associated with the investigation.
    --fax <fax number>    The fax number of a person associated with the investigation.
    --address <adress>    The address of a person associated with the investigation.
    --affiliation <affiliation>
                          The organization affiliation for a person associated with the investigation.
    --roles <roles>       Term to classify the role(s) performed by this person in the context of the investigation, which
                          means that the roles reported here need not correspond to roles held withing their affiliated
                          organization. Multiple annotations or values attached to one person can be provided by using a
                          semicolon (";") Unicode (U0003+B) as a separator (e.g.: submitter;funder;sponsor). The term can be
                          free text or from, for example, a controlled vocabulary or an ontology. If the latter source is used
                          the Term Accession Number and Term Source REF fields below are required.
    --rolestermaccessionnumber <roles term accession number>
                          The accession number from the Term Source associated with the selected term.
    --rolestermsourceref <roles term source ref>
                          dentifies the controlled vocabulary or ontology that this term comes from. The Source REF has to
                          match one of the Term Source Names declared in the Ontology Source Reference section.
    --help                display this list of options.
```


##### investigation person unregister

```powershell
USAGE: arc investigation person register [--help] --lastname <last name> --firstname <first name>
                                                      [--midinitials <mid initials>] [--email <e mail>]
                                                      [--phone <phone number>] [--fax <fax number>] [--address <adress>]
                                                      [--affiliation <affiliation>] [--roles <roles>]
                                                      [--rolestermaccessionnumber <roles term accession number>]
                                                      [--rolestermsourceref <roles term source ref>]

OPTIONS:

    --lastname, -l <last name>
                          The last name of a person associated with the investigation.
    --firstname, -f <first name>
                          The first name of a person associated with the investigation.
    --midinitials, -m <mid initials>
                          The middle initials of a person associated with the investigation.
    --email <e mail>      The email address of a person associated with the investigation.
    --phone <phone number>
                          The telephone number of a person associated with the investigation.
    --fax <fax number>    The fax number of a person associated with the investigation.
    --address <adress>    The address of a person associated with the investigation.
    --affiliation <affiliation>
                          The organization affiliation for a person associated with the investigation.
    --roles <roles>       Term to classify the role(s) performed by this person in the context of the investigation, which
                          means that the roles reported here need not correspond to roles held withing their affiliated
                          organization. Multiple annotations or values attached to one person can be provided by using a
                          semicolon (";") Unicode (U0003+B) as a separator (e.g.: submitter;funder;sponsor). The term can be
                          free text or from, for example, a controlled vocabulary or an ontology. If the latter source is used
                          the Term Accession Number and Term Source REF fields below are required.
    --rolestermaccessionnumber <roles term accession number>
                          The accession number from the Term Source associated with the selected term.
    --rolestermsourceref <roles term source ref>
                          dentifies the controlled vocabulary or ontology that this term comes from. The Source REF has to
                          match one of the Term Source Names declared in the Ontology Source Reference section.
    --help                display this list of options.
```

##### investigation person show

```powershell
USAGE: arc investigation person show [--help] --lastname <last name> --firstname <first name>
                                                 [--midinitials <mid initials>]

OPTIONS:

    --lastname, -l <last name>
                          The last name of a person associated with the investigation.
    --firstname, -f <first name>
                          The first name of a person associated with the investigation.
    --midinitials, -m <mid initials>
                          The middle initials of a person associated with the investigation.
    --help                display this list of options.
```

<br>

##### investigation publication

```powershell
USAGE: arc investigation publication [--help] [<subcommand> [<options>]]

SUBCOMMANDS:

    update <update args>  Update an existing publication in the arc investigation with the given publication metadata. The
                          publication is identified by the doi
    edit <edit args>      Open and edit an existing publication in the arc investigation with a text editor. The publication
                          is identified by the doi
    register <register args>
                          Register a publication in the arc investigation with the given assay metadata.
    unregister <remove args>
                          Unregister a publication from the given investigation. The publication is identified by the doi
    show <show args>      Show the metadata of a publication registered in the arc investigation
    list                  List all publication registered in the arc investigation

    Use 'arc <subcommand> --help' for additional information.

OPTIONS:

    --help                display this list of options.    
```

##### investigation publication update

```powershell
USAGE: arc investigation publication update [--help] --doi <doi> [--pubmedid <pubmed id>]
                                                         [--authorlist <author list>] [--title <publication title>]
                                                         [--status <publication status>]
                                                         [--statustermaccessionnumber <publication status term accession number>]
                                                         [--statustermsourceref <publication status term source ref>]

OPTIONS:

    --doi, -d <doi>       A Digital Object Identifier (DOI) for that publication (where available).
    --pubmedid, -p <pubmed id>
                          The PubMed IDs of the described publication(s) associated with this investigation.
    --authorlist <author list>
                          The list of authors associated with that publication.
    --title <publication title>
                          The title of publication associated with the investigation.
    --status <publication status>
                          A term describing the status of that publication (i.e. submitted, in preparation, published).
    --statustermaccessionnumber <publication status term accession number>
                          The accession number from the Term Source associated with the selected term.
    --statustermsourceref <publication status term source ref>
                          Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to
                          match one the Term Source Name declared in the in the Ontology Source Reference section.
    --help                display this list of options.    
```

##### investigation publication edit

```powershell
USAGE: arc investigation publication edit [--help] --doi <doi>

OPTIONS:

    --doi, -d <doi>       A Digital Object Identifier (DOI) for that publication (where available).
    --help                display this list of options.    
```

##### investigation publication register

```powershell
USAGE: arc investigation publication register [--help] --doi <doi> [--pubmedid <pubmed id>]
                                                           [--authorlist <author list>] [--title <publication title>]
                                                           [--status <publication status>]
                                                           [--statustermaccessionnumber <publication status term accession number>]
                                                           [--statustermsourceref <publication status term source ref>]

OPTIONS:

    --doi, -d <doi>       A Digital Object Identifier (DOI) for that publication (where available).
    --pubmedid, -p <pubmed id>
                          The PubMed IDs of the described publication(s) associated with this investigation.
    --authorlist <author list>
                          The list of authors associated with that publication.
    --title <publication title>
                          The title of publication associated with the investigation.
    --status <publication status>
                          A term describing the status of that publication (i.e. submitted, in preparation, published).
    --statustermaccessionnumber <publication status term accession number>
                          The accession number from the Term Source associated with the selected term.
    --statustermsourceref <publication status term source ref>
                          Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to
                          match one the Term Source Name declared in the in the Ontology Source Reference section.
    --help                display this list of options.    
```

##### investigation publication unregister

```powershell
USAGE: arc investigation publication unregister [--help] --doi <doi>

OPTIONS:

    --doi, -d <doi>       A Digital Object Identifier (DOI) for that publication (where available).
    --help                display this list of options.    
```

##### investigation publication show

```powershell
USAGE: arc investigation publication show [--help] --doi <doi>

OPTIONS:

    --doi, -d <doi>       A Digital Object Identifier (DOI) for that publication (where available).
    --help                display this list of options.    
```

<br>

#### study:

```powershell
USAGE: arc study [--help] [<subcommand> [<options>]]

SUBCOMMANDS:

    init <init args>      Initialize a new empty study file in the arc
    register <register args>
                          Register an existing study in the arc with the given assay metadata.
    add <add args>        Create a new study file in the arc and subsequently register it with the given study metadata
    delete <delete args>  Delete a study from the arc file structure
    unregister <unregister args>
                          Unregister a study from the arc investigation file
    remove <remove args>  Remove a study from the arc
    update <update args>  Update an existing study in the arc with the given study metadata
    edit <edit args>      Open and edit an existing study in the arc with a text editor. Arguments passed for this command
                          will be pre-set in the editor.
    show <show args>      Show the values of a study
    list                  List all studies registered in the arc
    person <person verbs> Person functions
    publication <publication verbs>
                          Publication functions
    design <design verbs> Design functions
    factor <factor verbs> Factor functions
    protocol <protocol verbs>
                          Protocol functions

    Use 'arc <subcommand> --help' for additional information.

OPTIONS:

    --help                display this list of options.
```

##### study init

```powershell
USAGE: arc study init [--help] --identifier <study identifier>

OPTIONS:

    --identifier <study identifier>
                          A unique identifier, either a temporary identifier supplied by users or one generated by a
                          repository or other database. For example, it could be an identifier complying with the LSID
                          specification.
    --help                display this list of options.
```

##### study register

```powershell
USAGE: arc study register [--help] --identifier <study identifier> [--title <title>] [--description <description>]
                                       [--submissiondate <submission date>] [--publicreleasedate <public release date>]

OPTIONS:

    --identifier <study identifier>
                          A unique identifier, either a temporary identifier supplied by users or one generated by a
                          repository or other database. For example, it could be an identifier complying with the LSID
                          specification.
    --title <title>       A concise phrase used to encapsulate the purpose and goal of the study.
    --description <description>
                          A textual description of the study, with components such as objective or goals.
    --submissiondate <submission date>
                          The date on which the study is submitted to an archive.
    --publicreleasedate <public release date>
                          The date on which the study SHOULD be released publicly.
    --help                display this list of options.
```

##### study add

```powershell
USAGE: arc study add [--help] --identifier <study identifier> [--title <title>] [--description <description>]
                                  [--submissiondate <submission date>] [--publicreleasedate <public release date>]

OPTIONS:

    --identifier <study identifier>
                          A unique identifier, either a temporary identifier supplied by users or one generated by a
                          repository or other database. For example, it could be an identifier complying with the LSID
                          specification.
    --title <title>       A concise phrase used to encapsulate the purpose and goal of the study.
    --description <description>
                          A textual description of the study, with components such as objective or goals.
    --submissiondate <submission date>
                          The date on which the study is submitted to an archive.
    --publicreleasedate <public release date>
                          The date on which the study SHOULD be released publicly.
    --help                display this list of options.
```

##### study delete

```powershell
USAGE: arc study delete [--help] --identifier <study identifier>

OPTIONS:

    --identifier <study identifier>
                          A unique identifier, either a temporary identifier supplied by users or one generated by a
                          repository or other database. For example, it could be an identifier complying with the LSID
                          specification.
    --help                display this list of options.
```

##### study unregister

```powershell
USAGE: arc study unregister [--help] --identifier <study identifier>

OPTIONS:

    --identifier <study identifier>
                          A unique identifier, either a temporary identifier supplied by users or one generated by a
                          repository or other database. For example, it could be an identifier complying with the LSID
                          specification.
    --help                display this list of options.
```

##### study remove

```powershell
USAGE: arc study remove [--help] --identifier <study identifier>

OPTIONS:

    --identifier <study identifier>
                          A unique identifier, either a temporary identifier supplied by users or one generated by a
                          repository or other database. For example, it could be an identifier complying with the LSID
                          specification.
    --help                display this list of options.
```

##### study update

Give new metadata that overwrite the current metadata of a study.

```powershell
USAGE: arc study update [--help] --identifier <study identifier> [--title <title>] [--description <description>]
                                     [--submissiondate <submission date>] [--publicreleasedate <public release date>]

OPTIONS:

    --identifier <study identifier>
                          A unique identifier, either a temporary identifier supplied by users or one generated by a
                          repository or other database. For example, it could be an identifier complying with the LSID
                          specification.
    --title <title>       A concise phrase used to encapsulate the purpose and goal of the study.
    --description <description>
                          A textual description of the study, with components such as objective or goals.
    --submissiondate <submission date>
                          The date on which the study is submitted to an archive.
    --publicreleasedate <public release date>
                          The date on which the study SHOULD be released publicly.
    --help                display this list of options.
```

##### study edit

Take the current metadata of a study and change it.  
(While `study edit` opens the current metadata that can be altered by the user, `study update` will take a new set of metadata and overwrites the existing one)

```powershell
USAGE: arc study edit [--help] --identifier <study identifier>

OPTIONS:

    --identifier <study identifier>
                          A unique identifier, either a temporary identifier supplied by users or one generated by a
                          repository or other database. For example, it could be an identifier complying with the LSID
                          specification.
    --help                display this list of options.

```

##### study show

```powershell
USAGE: arc study show [--help] --identifier <study identifier>

OPTIONS:

    --identifier <study identifier>
                          A unique identifier, either a temporary identifier supplied by users or one generated by a
                          repository or other database. For example, it could be an identifier complying with the LSID
                          specification.
    --help                display this list of options.
```

<br>

##### study person

```powershell
USAGE: arc study person [--help] [<subcommand> [<options>]]

SUBCOMMANDS:

    update <update args>  Update an existing person in the arc investigation study with the given person metadata. The person
                          is identified by the full name (first name, last name, mid initials)
    edit <edit args>      Open and edit an existing person in the arc investigation study with a text editor. The person is
                          identified by the full name (first name, last name, mid initials)
    register <register args>
                          Register a person in the arc investigation study with the given assay metadata.
    unregister <remove args>
                          Unregister a person from the given investigation study. The person is identified by the full name
                          (first name, last name, mid initials).
    show <show args>      Show the metadata of a person registered in the arc investigation study
    list                  List all persons registered in the arc investigation

    Use 'arc <subcommand> --help' for additional information.

OPTIONS:

    --help                display this list of options.
```


##### study person update

```powershell
USAGE: arc study person update [--help] --studyidentifier <string> --lastname <last name> --firstname <first name>
                                            [--midinitials <mid initials>] [--email <e mail>] [--phone <phone number>]
                                            [--fax <fax number>] [--address <adress>] [--affiliation <affiliation>]
                                            [--roles <roles>] [--rolestermaccessionnumber <roles term accession number>]
                                            [--rolestermsourceref <roles term source ref>]

OPTIONS:

    --studyidentifier, -s <string>
                          Identifier of the study the person is associated with
    --lastname, -l <last name>
                          The last name of a person associated with the study.
    --firstname, -f <first name>
                          The first name of a person associated with the study.
    --midinitials, -m <mid initials>
                          The middle initials of a person associated with the study.
    --email <e mail>      The email address of a person associated with the study.
    --phone <phone number>
                          The telephone number of a person associated with the study.
    --fax <fax number>    The fax number of a person associated with the study.
    --address <adress>    The address of a person associated with the study.
    --affiliation <affiliation>
                          The organization affiliation for a person associated with the study.
    --roles <roles>       Term to classify the role(s) performed by this person in the context of the study, which means that
                          the roles reported here need not correspond to roles held withing their affiliated organization.
                          Multiple annotations or values attached to one person can be provided by using a semicolon (";")
                          Unicode (U0003+B) as a separator (e.g.: submitter;funder;sponsor) .The term can be free text or
                          from, for example, a controlled vocabulary or an ontology. If the latter source is used the Term
                          Accession Number and Term Source REF fields below are required.
    --rolestermaccessionnumber <roles term accession number>
                          The accession number from the Term Source associated with the selected term.
    --rolestermsourceref <roles term source ref>
                          dentifies the controlled vocabulary or ontology that this term comes from. The Source REF has to
                          match one of the Term Source Names declared in the Ontology Source Reference section.
    --help                display this list of options.
```


##### study person edit

```powershell
USAGE: arc study person edit [--help] --studyidentifier <string> --lastname <last name> --firstname <first name>
                                          [--midinitials <mid initials>]

OPTIONS:

    --studyidentifier, -s <string>
                          Identifier of the study the person is associated with
    --lastname, -l <last name>
                          The last name of a person associated with the study.
    --firstname, -f <first name>
                          The first name of a person associated with the study.
    --midinitials, -m <mid initials>
                          The middle initials of a person associated with the study.
    --help                display this list of options.
```


##### study person register

```powershell
USAGE: arc study person register [--help] --studyidentifier <string> --lastname <last name>
                                              --firstname <first name> [--midinitials <mid initials>] [--email <e mail>]
                                              [--phone <phone number>] [--fax <fax number>] [--address <adress>]
                                              [--affiliation <affiliation>] [--roles <roles>]
                                              [--rolestermaccessionnumber <roles term accession number>]
                                              [--rolestermsourceref <roles term source ref>]

OPTIONS:

    --studyidentifier, -s <string>
                          Identifier of the study the person is associated with
    --lastname, -l <last name>
                          The last name of a person associated with the study.
    --firstname, -f <first name>
                          The first name of a person associated with the study.
    --midinitials, -m <mid initials>
                          The middle initials of a person associated with the study.
    --email <e mail>      The email address of a person associated with the study.
    --phone <phone number>
                          The telephone number of a person associated with the study.
    --fax <fax number>    The fax number of a person associated with the study.
    --address <adress>    The address of a person associated with the study.
    --affiliation <affiliation>
                          The organization affiliation for a person associated with the study.
    --roles <roles>       Term to classify the role(s) performed by this person in the context of the study, which means that
                          the roles reported here need not correspond to roles held withing their affiliated organization.
                          Multiple annotations or values attached to one person can be provided by using a semicolon (";")
                          Unicode (U0003+B) as a separator (e.g.: submitter;funder;sponsor) .The term can be free text or
                          from, for example, a controlled vocabulary or an ontology. If the latter source is used the Term
                          Accession Number and Term Source REF fields below are required.
    --rolestermaccessionnumber <roles term accession number>
                          The accession number from the Term Source associated with the selected term.
    --rolestermsourceref <roles term source ref>
                          dentifies the controlled vocabulary or ontology that this term comes from. The Source REF has to
                          match one of the Term Source Names declared in the Ontology Source Reference section.
    --help                display this list of options.
```


##### study person unregister

```powershell
USAGE: arc study person unregister [--help] --studyidentifier <string> --lastname <last name>
                                                --firstname <first name> [--midinitials <mid initials>]

OPTIONS:

    --studyidentifier, -s <string>
                          Identifier of the study the person is associated with
    --lastname, -l <last name>
                          The last name of a person associated with the study.
    --firstname, -f <first name>
                          The first name of a person associated with the study.
    --midinitials, -m <mid initials>
                          The middle initials of a person associated with the study.
    --help                display this list of options.
```


##### study person show

```powershell
USAGE: arc study person show [--help] --studyidentifier <string> --lastname <last name> --firstname <first name>
                                         [--midinitials <mid initials>]

OPTIONS:

    --studyidentifier, -s <string>
                          Identifier of the study the person is associated with
    --lastname, -l <last name>
                          The last name of a person associated with the study.
    --firstname, -f <first name>
                          The first name of a person associated with the study.
    --midinitials, -m <mid initials>
                          The middle initials of a person associated with the study.
    --help                display this list of options.
```
<br>

##### study publication 

```powershell
USAGE: arc study publication [--help] [<subcommand> [<options>]]

SUBCOMMANDS:

    update <update args>  Update an existing publication in the arc investigation study with the given publication metadata.
                          The publication is identified by the doi
    edit <edit args>      Open and edit an existing publication in the arc investigation study with a text editor. The
                          publication is identified by the doi
    register <register args>
                          Register a publication in the arc investigation study with the given assay metadata.
    unregister <remove args>
                          Unregister a publication from the given investigation study. The publication is identified by the doi
    show <show args>      Show the metadata of a publication registered in the arc investigation study
    list                  List all publication registered in the arc investigation study

    Use 'arc <subcommand> --help' for additional information.

OPTIONS:

    --help                display this list of options.
```

##### study publication update

```powershell
USAGE: arc study publication update [--help] --studyidentifier <string> --doi <doi> [--pubmedid <pubmed id>]
                                                 [--authorlist <author list>] [--title <publication title>]
                                                 [--status <publication status>]
                                                 [--statustermaccessionnumber <publication status term accession number>]
                                                 [--statustermsourceref <publication status term source ref>]

OPTIONS:

    --studyidentifier, -s <string>
                          Identifier of the study the publication is associated with
    --doi, -d <doi>       A Digital Object Identifier (DOI) for that publication (where available).
    --pubmedid, -p <pubmed id>
                          The PubMed IDs of the described publication(s) associated with this study.
    --authorlist <author list>
                          The list of authors associated with that publication.
    --title <publication title>
                          The title of publication associated with the study.
    --status <publication status>
                          A term describing the status of that publication (i.e. submitted, in preparation, published).
    --statustermaccessionnumber <publication status term accession number>
                          The accession number from the Term Source associated with the selected term.
    --statustermsourceref <publication status term source ref>
                          Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to
                          match one the Term Source Name declared in the in the Ontology Source Reference section.
    --help                display this list of options.
```

##### study publication edit

```powershell
USAGE: arc study publication edit [--help] --studyidentifier <string> --doi <doi>

OPTIONS:

    --studyidentifier, -s <string>
                          Identifier of the study the publication is associated with
    --doi, -d <doi>       A Digital Object Identifier (DOI) for that publication (where available).
    --help                display this list of options.
```

##### study publication register

```powershell
USAGE: arc study publication register [--help] --studyidentifier <string> --doi <doi> [--pubmedid <pubmed id>]
                                                   [--authorlist <author list>] [--title <publication title>]
                                                   [--status <publication status>]
                                                   [--statustermaccessionnumber <publication status term accession number>]
                                                   [--statustermsourceref <publication status term source ref>]

OPTIONS:

    --studyidentifier, -s <string>
                          Identifier of the study the publication is associated with
    --doi, -d <doi>       A Digital Object Identifier (DOI) for that publication (where available).
    --pubmedid, -p <pubmed id>
                          The PubMed IDs of the described publication(s) associated with this study.
    --authorlist <author list>
                          The list of authors associated with that publication.
    --title <publication title>
                          The title of publication associated with the study.
    --status <publication status>
                          A term describing the status of that publication (i.e. submitted, in preparation, published).
    --statustermaccessionnumber <publication status term accession number>
                          The accession number from the Term Source associated with the selected term.
    --statustermsourceref <publication status term source ref>
                          Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to
                          match one the Term Source Name declared in the in the Ontology Source Reference section.
    --help                display this list of options.
```

##### study publication unregister

```powershell
USAGE: arc study publication unregister [--help] --studyidentifier <string> --doi <doi>

OPTIONS:

    --studyidentifier, -s <string>
                          Identifier of the study the publication is associated with
    --doi, -d <doi>       A Digital Object Identifier (DOI) for that publication (where available).
    --help                display this list of options.
```

##### study publication show

```powershell
USAGE: arc study publication show [--help] --studyidentifier <string> --doi <doi>

OPTIONS:

    --studyidentifier, -s <string>
                          Identifier of the study the publication is associated with
    --doi, -d <doi>       A Digital Object Identifier (DOI) for that publication (where available).
    --help                display this list of options.
```


<br>

##### study design

```powershell
USAGE: arc study design [--help] [<subcommand> [<options>]]

SUBCOMMANDS:

    update <update args>  Update an existing design in the arc investigation study with the given publication metadata. The
                          publication is identified by the design type
    edit <edit args>      Open and edit an existing design in the arc investigation study with a text editor. The publication
                          is identified by the design type
    register <register args>
                          Register a design in the arc investigation study with the given assay metadata.
    unregister <remove args>
                          Unregister a design from the given investigation study. The publication is identified by the design
                          type
    show <show args>      Show the metadata of a design registered in the arc investigation study
    list                  List all design registered in the arc investigation study

    Use 'arc <subcommand> --help' for additional information.

OPTIONS:

    --help                display this list of options.
```

##### study design update

```powershell
USAGE: arc study design update [--help] --studyidentifier <string> --designtype <design type>
                                            [--typetermaccessionnumber <type term accession number>]
                                            [--typetermsourceref <type term source ref>]

OPTIONS:

    --studyidentifier, -s <string>
                          Identifier of the study the design is associated with
    --designtype, -d <design type>
                          A term allowing the classification of the study based on the overall experimental design, e.g
                          cross-over design or parallel group design. The term can be free text or from, for example, a
                          controlled vocabulary or an ontology. If the latter source is used the Term Accession Number and
                          Term Source REF fields below are required.
    --typetermaccessionnumber <type term accession number>
                          The accession number from the Term Source associated with the selected term.
    --typetermsourceref <type term source ref>
                          Identifies the controlled vocabulary or ontology that this term comes from. The Study Design Term
                          Source REF has to match one the Term Source Name declared in the Ontology Source Reference section.
    --help                display this list of options.
```

##### study design edit

```powershell
USAGE: arc study design edit [--help] --studyidentifier <string> --designtype <design type>

OPTIONS:

    --studyidentifier, -s <string>
                          Identifier of the study the design is associated with
    --designtype, -d <design type>
                          A term allowing the classification of the study based on the overall experimental design, e.g
                          cross-over design or parallel group design. The term can be free text or from, for example, a
                          controlled vocabulary or an ontology. If the latter source is used the Term Accession Number and
                          Term Source REF fields below are required.
    --help                display this list of options.
```

##### study design register

```powershell
USAGE: arc study design register [--help] --studyidentifier <string> --designtype <design type>
                                              [--typetermaccessionnumber <type term accession number>]
                                              [--typetermsourceref <type term source ref>]

OPTIONS:

    --studyidentifier, -s <string>
                          Identifier of the study the design is associated with
    --designtype, -d <design type>
                          A term allowing the classification of the study based on the overall experimental design, e.g
                          cross-over design or parallel group design. The term can be free text or from, for example, a
                          controlled vocabulary or an ontology. If the latter source is used the Term Accession Number and
                          Term Source REF fields below are required.
    --typetermaccessionnumber <type term accession number>
                          The accession number from the Term Source associated with the selected term.
    --typetermsourceref <type term source ref>
                          Identifies the controlled vocabulary or ontology that this term comes from. The Study Design Term
                          Source REF has to match one the Term Source Name declared in the Ontology Source Reference section.
    --help                display this list of options.
```

##### study design unregister

```powershell
USAGE: arc study design unregister [--help] --studyidentifier <string> --designtype <design type>

OPTIONS:

    --studyidentifier, -s <string>
                          Identifier of the study the design is associated with
    --designtype, -d <design type>
                          A term allowing the classification of the study based on the overall experimental design, e.g
                          cross-over design or parallel group design. The term can be free text or from, for example, a
                          controlled vocabulary or an ontology. If the latter source is used the Term Accession Number and
                          Term Source REF fields below are required.
    --help                display this list of options.
```

##### study design show

```powershell
USAGE: arc study design show [--help] --studyidentifier <string> --designtype <design type>

OPTIONS:

    --studyidentifier, -s <string>
                          Identifier of the study the design is associated with
    --designtype, -d <design type>
                          A term allowing the classification of the study based on the overall experimental design, e.g
                          cross-over design or parallel group design. The term can be free text or from, for example, a
                          controlled vocabulary or an ontology. If the latter source is used the Term Accession Number and
                          Term Source REF fields below are required.
    --help                display this list of options.
```
<br>

##### study factor

```powershell
USAGE: arc study factor [--help] [<subcommand> [<options>]]

SUBCOMMANDS:

    update <update args>  Update an existing factor in the arc investigation study with the given publication metadata. The
                          publication is identified by name
    edit <edit args>      Open and edit an existing factor in the arc investigation study with a text editor. The publication
                          is identified by name
    register <register args>
                          Register a factor in the arc investigation study with the given assay metadata.
    unregister <remove args>
                          Unregister a factor from the given investigation study. The publication is identified by name
    show <show args>      Show the metadata of a factor registered in the arc investigation study
    list                  List all factor registered in the arc investigation study

    Use 'arc <subcommand> --help' for additional information.

OPTIONS:

    --help                display this list of options.
```


##### study factor update

```powershell
USAGE: arc study factor update [--help] --studyidentifier <string> --name <name> [--factortype <factor type>]
                                            [--typetermaccessionnumber <type term accession number>]
                                            [--typetermsourceref <type term source ref>]

OPTIONS:

    --studyidentifier, -s <string>
                          Identifier of the study the design is associated with
    --name, -n <name>     The name of one factor used in the Study and/or Assay files. A factor corresponds to an independent
                          variable manipulated by the experimentalist with the intention to affect biological systems in a way
                          that can be measured by an assay. The value of a factor is given in the Study or Assay file,
                          accordingly. If both Study and Assay have a Factor Value, these must be different.
    --factortype <factor type>
                          A term allowing the classification of this factor into categories. The term can be free text or
                          from, for example, a controlled vocabulary or an ontology. If the latter source is used the Term
                          Accession Number and Term Source REF fields below are required.
    --typetermaccessionnumber <type term accession number>
                          The accession number from the Term Source associated with the selected term.
    --typetermsourceref <type term source ref>
                          Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to
                          match one of the Term Source Name declared in the Ontology Source Reference section.
    --help                display this list of options.
```


##### study factor edit

```powershell
USAGE: arc study factor edit [--help] --studyidentifier <string> --name <name>

OPTIONS:

    --studyidentifier, -s <string>
                          Identifier of the study the design is associated with
    --name, -n <name>     The name of one factor used in the Study and/or Assay files. A factor corresponds to an independent
                          variable manipulated by the experimentalist with the intention to affect biological systems in a way
                          that can be measured by an assay. The value of a factor is given in the Study or Assay file,
                          accordingly. If both Study and Assay have a Factor Value, these must be different.
    --help                display this list of options.
```


##### study factor register

```powershell
USAGE: arc study factor register [--help] --studyidentifier <string> --name <name> [--factortype <factor type>]
                                              [--typetermaccessionnumber <type term accession number>]
                                              [--typetermsourceref <type term source ref>]

OPTIONS:

    --studyidentifier, -s <string>
                          Identifier of the study the design is associated with
    --name, -n <name>     The name of one factor used in the Study and/or Assay files. A factor corresponds to an independent
                          variable manipulated by the experimentalist with the intention to affect biological systems in a way
                          that can be measured by an assay. The value of a factor is given in the Study or Assay file,
                          accordingly. If both Study and Assay have a Factor Value, these must be different.
    --factortype <factor type>
                          A term allowing the classification of this factor into categories. The term can be free text or
                          from, for example, a controlled vocabulary or an ontology. If the latter source is used the Term
                          Accession Number and Term Source REF fields below are required.
    --typetermaccessionnumber <type term accession number>
                          The accession number from the Term Source associated with the selected term.
    --typetermsourceref <type term source ref>
                          Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to
                          match one of the Term Source Name declared in the Ontology Source Reference section.
    --help                display this list of options.
```


##### study factor unregister

```powershell
USAGE: arc study factor unregister [--help] --studyidentifier <string> --name <name>

OPTIONS:

    --studyidentifier, -s <string>
                          Identifier of the study the design is associated with
    --name, -n <name>     The name of one factor used in the Study and/or Assay files. A factor corresponds to an independent
                          variable manipulated by the experimentalist with the intention to affect biological systems in a way
                          that can be measured by an assay. The value of a factor is given in the Study or Assay file,
                          accordingly. If both Study and Assay have a Factor Value, these must be different.
    --help                display this list of options.
```


##### study factor show

```powershell
USAGE: arc study factor show [--help] --studyidentifier <string> --name <name>

OPTIONS:

    --studyidentifier, -s <string>
                          Identifier of the study the design is associated with
    --name, -n <name>     The name of one factor used in the Study and/or Assay files. A factor corresponds to an independent
                          variable manipulated by the experimentalist with the intention to affect biological systems in a way
                          that can be measured by an assay. The value of a factor is given in the Study or Assay file,
                          accordingly. If both Study and Assay have a Factor Value, these must be different.
    --help                display this list of options.
```
<br>

##### study protocol

```powershell
USAGE: arc study protocol [--help] [<subcommand> [<options>]]

SUBCOMMANDS:

    update <update args>  Update an existing protocol in the arc investigation study with the given publication metadata. The
                          publication is identified by name
    edit <edit args>      Open and edit an existing protocol in the arc investigation study with a text editor. The
                          publication is identified by name
    register <register args>
                          Register a protocol in the arc investigation study with the given assay metadata.
    unregister <remove args>
                          Unregister a protocol from the given investigation study. The publication is identified by name
    show <show args>      Show the metadata of a protocol registered in the arc investigation study
    list                  List all protocol registered in the arc investigation study

    Use 'arc <subcommand> --help' for additional information.

OPTIONS:

    --help                display this list of options.
```

##### study protocol update

```powershell
USAGE: arc study protocol update [--help] --studyidentifier <string> --name <name>
                                              [--protocoltype <protocol type>]
                                              [--typetermaccessionnumber <type term accession number>]
                                              [--typetermsourceref <type term source ref>] [--description <description>]
                                              [--uri <uri>] [--version <version>] [--parametersname <parameters name>]
                                              [--parameterstermaccessionnumber <parameters term accession number>]
                                              [--parameterstermsourceref <parameters term source ref>]
                                              [--componentsname <compoments name>] [--componentstype <compoments type>]
                                              [--componentstypetermaccessionnumber <compoments type accession number>]
                                              [--componentstypetermsourceref <compoments type term source ref>]

OPTIONS:

    --studyidentifier, -s <string>
                          Identifier of the study the design is associated with
    --name, -n <name>     The name of the protocols used within the ISA-Tab document. The names are used as identifiers within
                          the ISA-Tab document and will be referenced in the Study and Assay files in the Protocol REF
                          columns. Names can be either local identifiers, unique within the ISA Archive which contains them,
                          or fully qualified external accession numbers.
    --protocoltype <protocol type>
                          Term to classify the protocol. The term can be free text or from, for example, a controlled
                          vocabulary or an ontology. If the latter source is used the Term Accession Number and Term Source
                          REF fields below are required.
    --typetermaccessionnumber <type term accession number>
                          The accession number from the Term Source associated with the selected term.
    --typetermsourceref <type term source ref>
                          Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to
                          match one of the Term Source Name declared in the Ontology Source Reference section.
    --description <description>
                          A free-text description of the protocol.
    --uri <uri>           Pointer to protocol resources external to the ISA-Tab that can be accessed by their Uniform Resource
                          Identifier (URI).
    --version <version>   An identifier for the version to ensure protocol tracking.
    --parametersname <parameters name>
                          A semicolon-delimited (";") list of parameter names, used as an identifier within the ISA-Tab
                          document. These names are used in the Study and Assay files (in the "Parameter Value []" column
                          heading) to list the values used for each protocol parameter. Refer to section Multiple values
                          fields in the Investigation File on how to encode multiple values in one field and match term sources
    --parameterstermaccessionnumber <parameters term accession number>
                          The accession number from the Term Source associated with the selected term.
    --parameterstermsourceref <parameters term source ref>
                          Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to
                          match one of the Term Source Name declared in the Ontology Source Reference section.
    --componentsname <compoments name>
                          A semicolon-delimited (";") list of a protocol's components; e.g. instrument names, software names,
                          and reagents names. Refer to section Multiple values fields in the Investigation File on how to
                          encode multiple components in one field and match term sources.
    --componentstype <compoments type>
                          Term to classify the protocol components listed for example, instrument, software, detector or
                          reagent. The term can be free text or from, for example, a controlled vocabulary or an ontology. If
                          the latter source is used the Term Accession Number and Term Source REF fields below are required.
    --componentstypetermaccessionnumber <compoments type accession number>
                          The accession number from the Source associated to the selected terms.
    --componentstypetermsourceref <compoments type term source ref>
                          Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to
                          match a Term Source Name previously declared in the ontology section.
    --help                display this list of options.
```

##### study protocol edit

```powershell
USAGE: arc study protocol edit [--help] --studyidentifier <string> --name <name>

OPTIONS:

    --studyidentifier, -s <string>
                          Identifier of the study the design is associated with
    --name, -n <name>     The name of one factor used in the Study and/or Assay files. A factor corresponds to an independent
                          variable manipulated by the experimentalist with the intention to affect biological systems in a way
                          that can be measured by an assay. The value of a factor is given in the Study or Assay file,
                          accordingly. If both Study and Assay have a Factor Value, these must be different.
    --help                display this list of options.
```

##### study protocol register

```powershell
USAGE: arc study protocol register [--help] --studyidentifier <string> --name <name>
                                                [--protocoltype <protocol type>]
                                                [--typetermaccessionnumber <type term accession number>]
                                                [--typetermsourceref <type term source ref>] [--description <description>]
                                                [--uri <uri>] [--version <version>] [--parametersname <parameters name>]
                                                [--parameterstermaccessionnumber <parameters term accession number>]
                                                [--parameterstermsourceref <parameters term source ref>]
                                                [--componentsname <compoments name>] [--componentstype <compoments type>]
                                                [--componentstypetermaccessionnumber <compoments type accession number>]
                                                [--componentstypetermsourceref <compoments type term source ref>]

OPTIONS:

    --studyidentifier, -s <string>
                          Identifier of the study the design is associated with
    --name, -n <name>     The name of the protocols used within the ISA-Tab document. The names are used as identifiers within
                          the ISA-Tab document and will be referenced in the Study and Assay files in the Protocol REF
                          columns. Names can be either local identifiers, unique within the ISA Archive which contains them,
                          or fully qualified external accession numbers.
    --protocoltype <protocol type>
                          Term to classify the protocol. The term can be free text or from, for example, a controlled
                          vocabulary or an ontology. If the latter source is used the Term Accession Number and Term Source
                          REF fields below are required.
    --typetermaccessionnumber <type term accession number>
                          The accession number from the Term Source associated with the selected term.
    --typetermsourceref <type term source ref>
                          Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to
                          match one of the Term Source Name declared in the Ontology Source Reference section.
    --description <description>
                          A free-text description of the protocol.
    --uri <uri>           Pointer to protocol resources external to the ISA-Tab that can be accessed by their Uniform Resource
                          Identifier (URI).
    --version <version>   An identifier for the version to ensure protocol tracking.
    --parametersname <parameters name>
                          A semicolon-delimited (";") list of parameter names, used as an identifier within the ISA-Tab
                          document. These names are used in the Study and Assay files (in the "Parameter Value []" column
                          heading) to list the values used for each protocol parameter. Refer to section Multiple values
                          fields in the Investigation File on how to encode multiple values in one field and match term sources
    --parameterstermaccessionnumber <parameters term accession number>
                          The accession number from the Term Source associated with the selected term.
    --parameterstermsourceref <parameters term source ref>
                          Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to
                          match one of the Term Source Name declared in the Ontology Source Reference section.
    --componentsname <compoments name>
                          A semicolon-delimited (";") list of a protocol's components; e.g. instrument names, software names,
                          and reagents names. Refer to section Multiple values fields in the Investigation File on how to
                          encode multiple components in one field and match term sources.
    --componentstype <compoments type>
                          Term to classify the protocol components listed for example, instrument, software, detector or
                          reagent. The term can be free text or from, for example, a controlled vocabulary or an ontology. If
                          the latter source is used the Term Accession Number and Term Source REF fields below are required.
    --componentstypetermaccessionnumber <compoments type accession number>
                          The accession number from the Source associated to the selected terms.
    --componentstypetermsourceref <compoments type term source ref>
                          Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to
                          match a Term Source Name previously declared in the ontology section.
    --help                display this list of options.
```

##### study protocol unregister

```powershell
USAGE: arc study protocol unregister [--help] --studyidentifier <string> --name <name>

OPTIONS:

    --studyidentifier, -s <string>
                          Identifier of the study the design is associated with
    --name, -n <name>     The name of one factor used in the Study and/or Assay files. A factor corresponds to an independent
                          variable manipulated by the experimentalist with the intention to affect biological systems in a way
                          that can be measured by an assay. The value of a factor is given in the Study or Assay file,
                          accordingly. If both Study and Assay have a Factor Value, these must be different.
    --help                display this list of options.
```

##### study protocol show

```powershell
USAGE: arc study protocol show [--help] --studyidentifier <string> --name <name>

OPTIONS:

    --studyidentifier, -s <string>
                          Identifier of the study the design is associated with
    --name, -n <name>     The name of one factor used in the Study and/or Assay files. A factor corresponds to an independent
                          variable manipulated by the experimentalist with the intention to affect biological systems in a way
                          that can be measured by an assay. The value of a factor is given in the Study or Assay file,
                          accordingly. If both Study and Assay have a Factor Value, these must be different.
    --help                display this list of options.
```


<br>

#### assay:

```powershell
USAGE: arc assay [--help] [<subcommand> [<options>]]

SUBCOMMANDS:

    init <init args>      Initialize a new empty assay and associated folder structure in the arc.
    register <register args>
                          Register an existing assay in the arc with the given assay metadata.
    add <add args>        Create a new assay file and associated folder structure in the arc and subsequently register it with
                          the given assay metadata
    delete <delete args>  Delete the given assays folder and its underlying file structure
    unregister <unregister args>
                          Unregister an assay from the given studys' assay register in the investigation file
    remove <remove args>  Both unregister and assay from the investigation file and delete its folders and files
    update <update args>  Update an existing assay in the arc with the given assay metadata
    edit <edit args>      Open and edit an existing assay in the arc with a text editor. Arguments passed for this command
                          will be pre-set in the editor.
    move <move args>      Move an assay from one study to another
    show <show args>      Show the values of an existing assay
    list                  List all assays registered in the arc

    Use 'arc <subcommand> --help' for additional information.

OPTIONS:

    --help                display this list of options.
```

##### assay init

```powershell
USAGE: arc assay init [--help] --assayidentifier <assay identifier>

OPTIONS:

    --assayidentifier, -a <assay identifier>
                          Identifier of the assay, will be used as name of the root folder of the new assay folder structure
    --help                display this list of options.
```


##### assay register

```powershell
USAGE: arc assay register [--help] [--studyidentifier <string>] --assayidentifier <string>
                                       [--measurementtype <measurement type>]
                                       [--measurementtypetermaccessionnumber <measurement type accession>]
                                       [--measurementtypetermsourceref <measurement type term source>]
                                       [--technologytype <technology type>]
                                       [--technologytypetermaccessionnumber <technology type accession>]
                                       [--technologytypetermsourceref <technology type term source>]
                                       [--technologyplatform <technology platform>]

OPTIONS:

    --studyidentifier, -s <string>
                          Name of the study in which the assay is situated
    --assayidentifier, -a <string>
                          Name of the assay of interest
    --measurementtype <measurement type>
                          A term to qualify the endpoint, or what is being measured (e.g. gene expression profiling or protein
                          identification). The term can be free text or from, for example, a controlled vocabulary or an
                          ontology. If the latter source is used the Term Accession Number and Term Source REF fields below
                          are required.
    --measurementtypetermaccessionnumber <measurement type accession>
                          The accession number from the Term Source associated with the selected term.
    --measurementtypetermsourceref <measurement type term source>
                          The Source REF has to match one of the Term Source Name declared in the Ontology Source Reference
                          section.
    --technologytype <technology type>
                          Term to identify the technology used to perform the measurement, e.g. DNA microarray, mass
                          spectrometry. The term can be free text or from, for example, a controlled vocabulary or an
                          ontology. If the latter source is used the Term Accession Number and Term Source REF fields below
                          are required.
    --technologytypetermaccessionnumber <technology type accession>
                          The accession number from the Term Source associated with the selected term.
    --technologytypetermsourceref <technology type term source>
                          Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to
                          match one of the Term Source Names declared in the Ontology Source Reference section.
    --technologyplatform <technology platform>
                          Manufacturer and platform name, e.g. Bruker AVANCE
    --help                display this list of options.
```


##### assay add

```powershell
USAGE: arc assay add [--help] [--studyidentifier <string>] --assayidentifier <string>
                                  [--measurementtype <measurement type>]
                                  [--measurementtypetermaccessionnumber <measurement type accession>]
                                  [--measurementtypetermsourceref <measurement type term source>]
                                  [--technologytype <technology type>]
                                  [--technologytypetermaccessionnumber <technology type accession>]
                                  [--technologytypetermsourceref <technology type term source>]
                                  [--technologyplatform <technology platform>]

OPTIONS:

    --studyidentifier, -s <string>
                          Name of the study in which the assay is situated
    --assayidentifier, -a <string>
                          Name of the assay of interest
    --measurementtype <measurement type>
                          A term to qualify the endpoint, or what is being measured (e.g. gene expression profiling or protein
                          identification). The term can be free text or from, for example, a controlled vocabulary or an
                          ontology. If the latter source is used the Term Accession Number and Term Source REF fields below
                          are required.
    --measurementtypetermaccessionnumber <measurement type accession>
                          The accession number from the Term Source associated with the selected term.
    --measurementtypetermsourceref <measurement type term source>
                          The Source REF has to match one of the Term Source Name declared in the Ontology Source Reference
                          section.
    --technologytype <technology type>
                          Term to identify the technology used to perform the measurement, e.g. DNA microarray, mass
                          spectrometry. The term can be free text or from, for example, a controlled vocabulary or an
                          ontology. If the latter source is used the Term Accession Number and Term Source REF fields below
                          are required.
    --technologytypetermaccessionnumber <technology type accession>
                          The accession number from the Term Source associated with the selected term.
    --technologytypetermsourceref <technology type term source>
                          Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to
                          match one of the Term Source Names declared in the Ontology Source Reference section.
    --technologyplatform <technology platform>
                          Manufacturer and platform name, e.g. Bruker AVANCE
    --help                display this list of options.
```


##### assay delete

```powershell
USAGE: arc assay delete [--help] --assayidentifier <assay identifier>

OPTIONS:

    --assayidentifier, -a <assay identifier>
                          Identifier of the assay, will be used as name of the root folder of the new assay folder structure
    --help                display this list of options.
```


##### assay unregister

```powershell
USAGE: arc assay unregister [--help] [--studyidentifier <study identifier>] --assayidentifier <assay identifier>

OPTIONS:

    --studyidentifier, -s <study identifier>
                          Identifier of the study in which the assay is registered
    --assayidentifier, -a <assay identifier>
                          Identifier of the assay of interest
    --help                display this list of options.
```


##### assay remove

```powershell
USAGE: arc assay remove [--help] [--studyidentifier <study identifier>] --assayidentifier <assay identifier>

OPTIONS:

    --studyidentifier, -s <study identifier>
                          Identifier of the study in which the assay is registered
    --assayidentifier, -a <assay identifier>
                          Identifier of the assay of interest
    --help                display this list of options.
```


##### assay update

Give new metadata that overwrite the current metadata of an assay.

```powershell
USAGE: arc assay update [--help] [--studyidentifier <string>] --assayidentifier <string>
                                     [--measurementtype <measurement type>]
                                     [--measurementtypetermaccessionnumber <measurement type accession>]
                                     [--measurementtypetermsourceref <measurement type term source>]
                                     [--technologytype <technology type>]
                                     [--technologytypetermaccessionnumber <technology type accession>]
                                     [--technologytypetermsourceref <technology type term source>]
                                     [--technologyplatform <technology platform>]

OPTIONS:

    --studyidentifier, -s <string>
                          Name of the study in which the assay is situated
    --assayidentifier, -a <string>
                          Name of the assay of interest
    --measurementtype <measurement type>
                          A term to qualify the endpoint, or what is being measured (e.g. gene expression profiling or protein
                          identification). The term can be free text or from, for example, a controlled vocabulary or an
                          ontology. If the latter source is used the Term Accession Number and Term Source REF fields below
                          are required.
    --measurementtypetermaccessionnumber <measurement type accession>
                          The accession number from the Term Source associated with the selected term.
    --measurementtypetermsourceref <measurement type term source>
                          The Source REF has to match one of the Term Source Name declared in the Ontology Source Reference
                          section.
    --technologytype <technology type>
                          Term to identify the technology used to perform the measurement, e.g. DNA microarray, mass
                          spectrometry. The term can be free text or from, for example, a controlled vocabulary or an
                          ontology. If the latter source is used the Term Accession Number and Term Source REF fields below
                          are required.
    --technologytypetermaccessionnumber <technology type accession>
                          The accession number from the Term Source associated with the selected term.
    --technologytypetermsourceref <technology type term source>
                          Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to
                          match one of the Term Source Names declared in the Ontology Source Reference section.
    --technologyplatform <technology platform>
                          Manufacturer and platform name, e.g. Bruker AVANCE
    --help                display this list of options.
```


##### assay edit

Take the current metadata of an assay and change it.  
(While `assay edit` opens the current metadata that can be altered by the user, `assay update` will take a new set of metadata and overwrites the existing one)

```powershell
USAGE: arc assay edit [--help] [--studyidentifier <study identifier>] --assayidentifier <assay identifier>

OPTIONS:

    --studyidentifier, -s <study identifier>
                          Identifier of the study in which the assay is registered
    --assayidentifier, -a <assay identifier>
                          Identifier of the assay of interest
    --help                display this list of options.
```

##### assay move

```powershell
USAGE: arc assay move [--help] --studyidentifier <study identifier> --assayidentifier <assay identifier>
                                   --targetstudyidentifier <target study identifier>

OPTIONS:

    --studyidentifier, -s <study identifier>
                          Name of the study in which the assay is situated
    --assayidentifier, -a <assay identifier>
                          Name of the assay of interest
    --targetstudyidentifier, -t <target study identifier>
                          Target study to which the assay should be moved
    --help                display this list of options.
```

##### assay show

```powershell
USAGE: arc assay show [--help] [--studyidentifier <study identifier>] --assayidentifier <assay identifier>

OPTIONS:

    --studyidentifier, -s <study identifier>
                          Identifier of the study in which the assay is registered
    --assayidentifier, -a <assay identifier>
                          Identifier of the assay of interest
    --help                display this list of options.
```
<br>

#### configuration:

```powershell
USAGE: arc configuration [--help] [<subcommand> [<options>]]

SUBCOMMANDS:

    edit <edit args>      Open and edit an existing assay in the arc with a text editor. Arguments passed for this command
                          will be pre-set in the editor.
    list <list args>      List all assays registered in the arc.
    set <set args>        Assign the given value to the given name.
    unset <unset args>    Remove the value bound to the given name.

    Use 'arc <subcommand> --help' for additional information.

OPTIONS:

    --help                display this list of options.
```

##### configuration list

```powershell
USAGE: arc configuration list [--help] [--local] [--global]

OPTIONS:

    --local, -l           Lists the local settings for this arc
    --global, -g          Lists the global settings of the arccommander
    --help                display this list of options.
```

##### configuration edit

```powershell
USAGE: arc configuration edit [--help] [--local] [--global]

OPTIONS:

    --local, -l           Edit the local settings for this arc
    --global, -g          Edit the global settings of the arccommander
    --help                display this list of options.
```

##### configuration set

```powershell
USAGE: arc configuration set [--help] [--local] [--global] --name <string> --value <string>

OPTIONS:

    --local, -l           Set the the value of the name locally for this arc
    --global, -g          Set the the value of the name globally for the arccommander
    --name, -n <string>   The name of the setting in 'Section.Key' format
    --value, -v <string>  The new value of the setting
    --help                display this list of options.
```

##### configuration unset

```powershell
USAGE: arc configuration unset [--help] [--local] [--global] --name <string>

OPTIONS:

    --local, -l           Unset the the value of the name locally for this arc
    --global, -g          Unset the the value of the name globally for the arccommander
    --name, -n <string>   The name of the setting in 'Section.Key' format
    --help                display this list of options.
```

