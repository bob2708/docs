---
editable: false
sourcePath: en/_api-ref-grpc/compute/v1/api-ref/grpc/Disk/listSnapshotSchedules.md
---

# Compute Cloud API, gRPC: DiskService.ListSnapshotSchedules {#ListSnapshotSchedules}

Retrieves the list of snapshot schedules the specified disk is attached to.

## gRPC request

**rpc ListSnapshotSchedules ([ListDiskSnapshotSchedulesRequest](#yandex.cloud.compute.v1.ListDiskSnapshotSchedulesRequest)) returns ([ListDiskSnapshotSchedulesResponse](#yandex.cloud.compute.v1.ListDiskSnapshotSchedulesResponse))**

## ListDiskSnapshotSchedulesRequest {#yandex.cloud.compute.v1.ListDiskSnapshotSchedulesRequest}

```json
{
  "diskId": "string",
  "pageSize": "int64",
  "pageToken": "string"
}
```

#|
||Field | Description ||
|| diskId | **string**

ID of the disk to list snapshot schedules for. ||
|| pageSize | **int64**

The maximum number of results per page to return. If the number of available
results is larger than `page_size`, the service returns a [ListDiskSnapshotSchedulesResponse.nextPageToken](#yandex.cloud.compute.v1.ListDiskSnapshotSchedulesResponse)
that can be used to get the next page of results in subsequent list requests.

Default value: 100. ||
|| pageToken | **string**

Page token. To get the next page of results, set `page_token` to the
[ListDiskSnapshotSchedulesResponse.nextPageToken](#yandex.cloud.compute.v1.ListDiskSnapshotSchedulesResponse) returned by a previous list request. ||
|#

## ListDiskSnapshotSchedulesResponse {#yandex.cloud.compute.v1.ListDiskSnapshotSchedulesResponse}

```json
{
  "snapshotSchedules": [
    {
      "id": "string",
      "folderId": "string",
      "createdAt": "google.protobuf.Timestamp",
      "name": "string",
      "description": "string",
      "labels": "string",
      "status": "Status",
      "schedulePolicy": {
        "startAt": "google.protobuf.Timestamp",
        "expression": "string"
      },
      // Includes only one of the fields `retentionPeriod`, `snapshotCount`
      "retentionPeriod": "google.protobuf.Duration",
      "snapshotCount": "int64",
      // end of the list of possible fields
      "snapshotSpec": {
        "description": "string",
        "labels": "string"
      }
    }
  ],
  "nextPageToken": "string"
}
```

#|
||Field | Description ||
|| snapshotSchedules[] | **[SnapshotSchedule](#yandex.cloud.compute.v1.SnapshotSchedule)**

List of snapshot schedules the specified disk is attached to. ||
|| nextPageToken | **string**

Token for getting the next page of the list. If the number of results is greater than
the specified [ListDiskSnapshotSchedulesRequest.pageSize](#yandex.cloud.compute.v1.ListDiskSnapshotSchedulesRequest), use `next_page_token` as the value
for the [ListDiskSnapshotSchedulesRequest.pageToken](#yandex.cloud.compute.v1.ListDiskSnapshotSchedulesRequest) parameter in the next list request.

Each subsequent page will have its own `next_page_token` to continue paging through the results. ||
|#

## SnapshotSchedule {#yandex.cloud.compute.v1.SnapshotSchedule}

A snapshot schedule. For details about the concept, see [documentation](/docs/compute/concepts/snapshot-schedule).

#|
||Field | Description ||
|| id | **string**

ID of the snapshot schedule. ||
|| folderId | **string**

ID of the folder that the snapshot schedule belongs to. ||
|| createdAt | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**

Creation timestamp. ||
|| name | **string**

Name of the snapshot schedule.

The name is unique within the folder. ||
|| description | **string**

Description of the snapshot schedule. ||
|| labels | **string**

Snapshot schedule labels as `key:value` pairs. ||
|| status | enum **Status**

Status of the snapshot schedule.

- `STATUS_UNSPECIFIED`
- `CREATING`: The snapshot schedule is being created.
- `ACTIVE`: The snapshot schedule is on: new disk snapshots will be created, old ones deleted
(if [SnapshotSchedule.retentionPolicy](/docs/compute/api-ref/grpc/Disk/listSnapshotSchedules#yandex.cloud.compute.v1.SnapshotSchedule.retentionPolicy) is specified).
- `INACTIVE`: The schedule is interrupted, snapshots won't be created or deleted.
- `DELETING`: The schedule is being deleted.
- `UPDATING`: Changes are being made to snapshot schedule settings or a list of attached disks. ||
|| schedulePolicy | **[SchedulePolicy](#yandex.cloud.compute.v1.SchedulePolicy)**

Frequency settings of the snapshot schedule. ||
|| retentionPeriod | **[google.protobuf.Duration](https://developers.google.com/protocol-buffers/docs/reference/csharp/class/google/protobuf/well-known-types/duration)**

Retention period of the snapshot schedule. Once a snapshot created by the schedule reaches this age, it is
automatically deleted.

Includes only one of the fields `retentionPeriod`, `snapshotCount`.

Retention policy of the snapshot schedule. ||
|| snapshotCount | **int64**

Retention count of the snapshot schedule. Once the number of snapshots created by the schedule exceeds this
number, the oldest ones are automatically deleted. E.g. if the number is 5, the first snapshot is deleted
after the sixth one is created, the second is deleted after the seventh one is created, and so on.

Includes only one of the fields `retentionPeriod`, `snapshotCount`.

Retention policy of the snapshot schedule. ||
|| snapshotSpec | **[SnapshotSpec](#yandex.cloud.compute.v1.SnapshotSpec)**

Attributes of snapshots created by the snapshot schedule. ||
|#

## SchedulePolicy {#yandex.cloud.compute.v1.SchedulePolicy}

A resource for frequency settings of a snapshot schedule.

#|
||Field | Description ||
|| startAt | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**

Timestamp for creating the first snapshot. ||
|| expression | **string**

Cron expression for the snapshot schedule (UTC+0).

The expression must consist of five fields (`Minutes Hours Day-of-month Month Day-of-week`) or be one of
nonstandard predefined expressions (e.g. `@hourly`). For details about the format,
see [documentation](/docs/compute/concepts/snapshot-schedule#cron) ||
|#

## SnapshotSpec {#yandex.cloud.compute.v1.SnapshotSpec}

A resource for attributes of snapshots created by the snapshot schedule.

#|
||Field | Description ||
|| description | **string**

Description of the created snapshot. ||
|| labels | **string**

Snapshot labels as `key:value` pairs. ||
|#