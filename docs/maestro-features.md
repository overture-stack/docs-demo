---
id: maestro-features
title: Features
sidebar_label: Features
---

##  Multiple SONGs, One Index
Maestro supports indexing from multiple metadata repositories [SONG](https://www.overture.bio/products/song).
Maestro can be connected to multiple SONGs and it will index all files into a single Elasticsearch index. Conflict resolution is built in as partof the indexing process. For example, if the same file was identified in multiple SONGs that are geographically distributed, then it will aggregate all repositories information in the same index document.

As an example, you can see in the `repositories` section of the following document that this file is found in multiple repositories:

``` json
   {
      "object_id": "9ce9358d",
      "access": "controlled",
      "study": "ABCD-CA",
      "analysis": {
        "id": "EGAZ",
        "type": "sequencingRead",
        "state": "PUBLISHED",
        "study": "ABCD-CA",
        "experiment": {
          "analysisId": "EGAZ",
          "aligned": true,
          "libraryStrategy": "WGS"
        }
      },
      "file": {
        "name": "b2e40ebb719e.bam",
        "format": "BAM",
        "md5sum": "b2e40ebb719e1754e99be2e752239639",
        "size": 77675501639,
        "last_modified": null,
        "index_file": {
          "object_id": "9ce9358d",
          "name": "b2e40eb_merged.mdup.bam.bai",
          "format": "BAI",
          "md5sum": "227a2a11d660a8a53a7375c6623034e2",
          "size": 8982928
        }
      },
      "repositories": [
        {
          "code": "collab",
          "organization": "ICGC",
          "name": "collaboratory",
          "type": "S3",
          "country": "CA",
          "base_url": "http://song.example.com",
          "data_path": "/oicr.icgc/data",
          "metadata_path": "/oicr.icgc.meta/metadata/464116e4"
        },
        {
          "code": "song2",
          "organization": "ICGC",
          "name": "song2 repo",
          "type": "S3",
          "country": "US",
          "base_url": "http://song2.example.com",
          "data_path": "/oicr.icgc/data",
          "metadata_path": "/oicr.icgc.meta/metadata/464116e4"
        }
      ],
      "donors": [
        {
          "id": "DO23",
          "submitted_id": "MDT-2",
          "specimen": {
            "id": "SP20",
            "type": "Normal - blood derived",
            "submitted_id": "MDT-_control_specimen",
            "sample": {
              "id": "SA60",
              "submitted_id": "MDT_control",
              "type": "DNA"
            }
          }
        }
      ]
    }
```

## Multiple indexing levels
In the data model, data is grouped by different entities.  Maestro can index discreet data levels. For example, indexing can be driven at a Repository, Study, or individual Analysis level.

## Different indexing APIs
- Event driven indexing: Kafka integration with SONG to index published analysis and delete suppressed / unpublished analyses, (see the [Usage](usage.md#kafka-topics) Kafka settings)
- HTTP json API see [Usage](usage.md#http-api)

## Ability to Exclude
You can configure the installation to exclude specific analyses by one of the following Ids: Study, Analysis, Donor, Sample Or file. (see the [Configurations](setup.md#configurations) exclusion rules section )

## Slack integration
You can configure Maestro to send specific notifications to a slack webhook integration
currently notifications are for errors during the indexing process.
