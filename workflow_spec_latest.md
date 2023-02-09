# BioImage.IO Workflow Resource Description File 0.2.3
This specification defines the fields used in a BioImage.IO-compliant resource description file (`RDF`) for describing workflows.
These fields are typically stored in a YAML file which we call Workflow Resource Description File or `workflow RDF`.

The workflow RDF YAML file contains mandatory and optional fields. In the following description, optional fields are indicated by _optional_.
_optional*_ with an asterisk indicates the field is optional depending on the value in another field.


* <a id="format_version"></a>`format_version` _(required String)_ Version of the BioImage.IO Resource Description File Specification used.The current general format version described here is 0.2.3. Note: The general RDF format is not to be confused with specialized RDF format like the Model RDF format.
* <a id="description"></a>`description` _(required String)_ A string containing a brief description.
* <a id="inputs"></a>`inputs` _(required List\[Input\])_ Describes the inputs expected by this workflow.
    1.  _(Input)_   is a Dict with the following keys:
        * <a id="inputs:name"></a>`name` _(String)_ Parameter name. No duplicates are allowed.
        * <a id="inputs:type"></a>`type` _(String)_ One of: ('tensor', 'int', 'float', 'string', 'boolean', 'list', 'dict', 'any')
        * <a id="inputs:axes"></a>`axes` _(Union\[List\[Axis\] | String\])_ Axis specifications (only required for type 'tensor').
            1.  _(List\[Axis\])_ 
                1.  _(Axis)_   is a Dict with the following keys:
                    * <a id="inputs:axes:type"></a>`type` _(String)_ One of: ('batch', 'channel', 'index', 'time', 'space')
                    * <a id="inputs:axes:description"></a>`description` _(String)_ Description of axis (max 128 characters).
                    * <a id="inputs:axes:name"></a>`name` _(Union\[String | List\[String\]\])_ A unique axis name (max 32 characters)
                        1.  _(String)_ Axis name. Indexed for channel axis, e.g. RGB -> RGB[0],RGB[1],RGB[2]
                        1.  _(List\[String\])_ For channel axis only: Name per channel, e.g. [red, green, blue]
                    * <a id="inputs:axes:scaling_factor"></a>`scaling_factor` _(Union\[Float | List\[Float\]\])_ For channel axis only: Scaling factor (per channel). Values are given in 'scaling_factor' 'unit'.
                        1.  _(Float)_ Scaling factor for all channels.
                        1.  _(List\[Float\])_ Scaling factor per channel.
                    * <a id="inputs:axes:step"></a>`step` _(Float)_ One 'pixel' along this axis corresponds to 'step' 'unit'. (Invalid for channel axis.)
                    * <a id="inputs:axes:unit"></a>`unit` _(Union\[String | List\[String\]\])_ Physical unit of this axis (max 32 characters).
                        1.  _(List\[String\])_ For channel axis only: unit of data values (max 32 characters; per channel if list).
            1.  _(String)_ Arbitrary or unknown combination of valid axis types.
        * <a id="inputs:description"></a>`description` _(String)_ Description (max 128 characters).
* <a id="name"></a>`name` _(required Name→String)_ name of the resource, a human-friendly name
* <a id="options"></a>`options` _(required List\[Option\])_ Describes the options that may be given to this workflow.
    1.  _(Option)_   is a Dict with the following keys:
        * <a id="options:default"></a>`default` _(Raw)_ Default value compatible with type given by `type` field.
            
            The `null` value is compatible with any specified type.
        * <a id="options:name"></a>`name` _(String)_ Parameter name. No duplicates are allowed.
        * <a id="options:type"></a>`type` _(String)_ One of: ('tensor', 'int', 'float', 'string', 'boolean', 'list', 'dict', 'any')
        * <a id="options:axes"></a>`axes` _(Union\[List\[Axis\] | String\])_ Axis specifications (only required for type 'tensor').
            1.  _(List\[Axis\])_ 
                1.  _(Axis)_   is a Dict with the following keys:
                    * <a id="options:axes:type"></a>`type` _(String)_ One of: ('batch', 'channel', 'index', 'time', 'space')
                    * <a id="options:axes:description"></a>`description` _(String)_ Description of axis (max 128 characters).
                    * <a id="options:axes:name"></a>`name` _(Union\[String | List\[String\]\])_ A unique axis name (max 32 characters)
                        1.  _(String)_ Axis name. Indexed for channel axis, e.g. RGB -> RGB[0],RGB[1],RGB[2]
                        1.  _(List\[String\])_ For channel axis only: Name per channel, e.g. [red, green, blue]
                    * <a id="options:axes:scaling_factor"></a>`scaling_factor` _(Union\[Float | List\[Float\]\])_ For channel axis only: Scaling factor (per channel). Values are given in 'scaling_factor' 'unit'.
                        1.  _(Float)_ Scaling factor for all channels.
                        1.  _(List\[Float\])_ Scaling factor per channel.
                    * <a id="options:axes:step"></a>`step` _(Float)_ One 'pixel' along this axis corresponds to 'step' 'unit'. (Invalid for channel axis.)
                    * <a id="options:axes:unit"></a>`unit` _(Union\[String | List\[String\]\])_ Physical unit of this axis (max 32 characters).
                        1.  _(List\[String\])_ For channel axis only: unit of data values (max 32 characters; per channel if list).
            1.  _(String)_ Arbitrary or unknown combination of valid axis types.
        * <a id="options:description"></a>`description` _(String)_ Description (max 128 characters).
* <a id="attachments"></a>`attachments` _(optional Attachments)_ Additional unknown keys are allowed. Attachments is a Dict with the following keys:
    * <a id="attachments:files"></a>`files` _(optional List\[Union\[URI→String | Path→String\]\])_ File attachments; included when packaging the resource.
* <a id="authors"></a>`authors` _(optional List\[Author\])_ A list of authors. The authors are the creators of the specifications and the primary points of contact.
    1.  _(Author)_   is a Dict with the following keys:
        * <a id="authors:affiliation"></a>`affiliation` _(String)_ Affiliation.
        * <a id="authors:github_user"></a>`github_user` _(String)_ GitHub user name.
        * <a id="authors:name"></a>`name` _(Name→String)_ Full name.
        * <a id="authors:orcid"></a>`orcid` _(String)_ [orcid](https://support.orcid.org/hc/en-us/sections/360001495313-What-is-ORCID) id in hyphenated groups of 4 digits, e.g. '0000-0001-2345-6789' (and [valid](https://support.orcid.org/hc/en-us/articles/360006897674-Structure-of-the-ORCID-Identifier) as per ISO 7064 11,2.)
* <a id="badges"></a>`badges` _(optional List\[Badge\])_ a list of badges
    1.  _(Badge)_ Custom badge. Badge is a Dict with the following keys:
        * <a id="badges:label"></a>`label` _(String)_ e.g. 'Open in Colab'
        * <a id="badges:icon"></a>`icon` _(String)_ e.g. 'https://colab.research.google.com/assets/colab-badge.svg'
        * <a id="badges:url"></a>`url` _(Union\[URL→URI | Path→String\])_ e.g. 'https://colab.research.google.com/github/HenriquesLab/ZeroCostDL4Mic/blob/master/Colab_notebooks/U-net_2D_ZeroCostDL4Mic.ipynb'
* <a id="cite"></a>`cite` _(optional List\[CiteEntry\])_ A list of citation entries.
    Each entry contains a mandatory `text` field and either one or both of `doi` and `url`.
    E.g. the citation for the model architecture and/or the training data used.
    1.  _(CiteEntry)_   is a Dict with the following keys:
        * <a id="cite:text"></a>`text` _(String)_ free text description
        * <a id="cite:doi"></a>`doi` _(DOI→String)_ digital object identifier, see https://www.doi.org/ (alternatively specify `url`)
        * <a id="cite:url"></a>`url` _(String)_ url to cite (alternatively specify `doi`)
* <a id="covers"></a>`covers` _(optional List\[Union\[URL→URI | Path→String\]\])_ A list of cover images provided by either a relative path to the model folder, or a hyperlink starting with 'http[s]'. Please use an image smaller than 500KB and an aspect ratio width to height of 2:1. The supported image formats are: 'jpg', 'png', 'gif'.
* <a id="documentation"></a>`documentation` _(optional Union\[URL→URI | Path→String\])_ URL or relative path to markdown file with additional documentation. For markdown files the recommended documentation file name is `README.md`.
* <a id="download_url"></a>`download_url` _(optional Union\[URL→URI | Path→String\])_ optional url to download the resource from
* <a id="git_repo"></a>`git_repo` _(optional URL→URI)_ A url to the git repository, e.g. to Github or Gitlab.
* <a id="icon"></a>`icon` _(optional String)_ an icon for the resource
* <a id="id"></a>`id` _(optional String)_ Unique id within a collection of resources.
* <a id="license"></a>`license` _(optional String)_ A [SPDX license identifier](https://spdx.org/licenses/)(e.g. `CC-BY-4.0`, `MIT`, `BSD-2-Clause`). We don't support custom license beyond the SPDX license list, if you need that please send an Github issue to discuss your intentions with the community.
* <a id="links"></a>`links` _(optional List\[String\])_ links to other bioimage.io resources
* <a id="maintainers"></a>`maintainers` _(optional List\[Maintainer\])_ Maintainers of this resource.
    1.  _(Maintainer)_   is a Dict with the following keys:
        * <a id="maintainers:affiliation"></a>`affiliation` _(String)_ Affiliation.
        * <a id="maintainers:github_user"></a>`github_user` _(String)_ GitHub user name.
        * <a id="maintainers:name"></a>`name` _(Name→String)_ Full name.
        * <a id="maintainers:orcid"></a>`orcid` _(String)_ [orcid](https://support.orcid.org/hc/en-us/sections/360001495313-What-is-ORCID) id in hyphenated groups of 4 digits, e.g. '0000-0001-2345-6789' (and [valid](https://support.orcid.org/hc/en-us/articles/360006897674-Structure-of-the-ORCID-Identifier) as per ISO 7064 11,2.)
* <a id="outputs"></a>`outputs` _(optional List\[Output\])_ Describes the outputs of this workflow.
    1.  _(Output)_   is a Dict with the following keys:
        * <a id="outputs:name"></a>`name` _(String)_ Parameter name. No duplicates are allowed.
        * <a id="outputs:type"></a>`type` _(String)_ One of: ('tensor', 'int', 'float', 'string', 'boolean', 'list', 'dict', 'any')
        * <a id="outputs:axes"></a>`axes` _(Union\[List\[Axis\] | String\])_ Axis specifications (only required for type 'tensor').
            1.  _(List\[Axis\])_ 
                1.  _(Axis)_   is a Dict with the following keys:
                    * <a id="outputs:axes:type"></a>`type` _(String)_ One of: ('batch', 'channel', 'index', 'time', 'space')
                    * <a id="outputs:axes:description"></a>`description` _(String)_ Description of axis (max 128 characters).
                    * <a id="outputs:axes:name"></a>`name` _(Union\[String | List\[String\]\])_ A unique axis name (max 32 characters)
                        1.  _(String)_ Axis name. Indexed for channel axis, e.g. RGB -> RGB[0],RGB[1],RGB[2]
                        1.  _(List\[String\])_ For channel axis only: Name per channel, e.g. [red, green, blue]
                    * <a id="outputs:axes:scaling_factor"></a>`scaling_factor` _(Union\[Float | List\[Float\]\])_ For channel axis only: Scaling factor (per channel). Values are given in 'scaling_factor' 'unit'.
                        1.  _(Float)_ Scaling factor for all channels.
                        1.  _(List\[Float\])_ Scaling factor per channel.
                    * <a id="outputs:axes:step"></a>`step` _(Float)_ One 'pixel' along this axis corresponds to 'step' 'unit'. (Invalid for channel axis.)
                    * <a id="outputs:axes:unit"></a>`unit` _(Union\[String | List\[String\]\])_ Physical unit of this axis (max 32 characters).
                        1.  _(List\[String\])_ For channel axis only: unit of data values (max 32 characters; per channel if list).
            1.  _(String)_ Arbitrary or unknown combination of valid axis types.
        * <a id="outputs:description"></a>`description` _(String)_ Description (max 128 characters).
* <a id="rdf_source"></a>`rdf_source` _(optional Union\[URL→URI | DOI→String\])_ url or doi to the source of the resource definition
* <a id="source"></a>`source` _(optional Union\[URI→String | Path→String\])_ url or local relative path to the source of the resource
* <a id="tags"></a>`tags` _(optional List\[String\])_ A list of tags.
* <a id="version"></a>`version` _(optional Version→String)_ The version number of the model. The version number format must be a string in `MAJOR.MINOR.PATCH` format following the guidelines in Semantic Versioning 2.0.0 (see https://semver.org/), e.g. the initial version number should be `0.1.0`.

