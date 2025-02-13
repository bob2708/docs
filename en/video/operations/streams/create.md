---
title: How to create a broadcast in {{ video-full-name }}
description: Follow this guide to create a {{ video-full-name }} broadcast.
---

# Creating a broadcast

{% list tabs group=instructions %}

- {{ video-name }} interface {#console}

   1. Open the {{ video-name }} [home page]({{ link-video-main }}).
   1. Select a channel.
   1. In the ![image](../../../_assets/console-icons/antenna-signal.svg) **{{ ui-key.yacloud_video.streams.title_streams }}** tab, click **{{ ui-key.yacloud_video.streams.action_create-stream }}**.
   1. Enter a name and description for the broadcast.
   1. Select or [create](../lines/create.md) a new line.
   1. In the **{{ ui-key.yacloud_video.thumbnails.label_thumbnail }}** field, click ![image](../../../_assets/console-icons/cloud-arrow-up-in.svg) **Select file** and select an image for the cover.

      {% include [image-characteristic](../../../_includes/video/image-characteristic.md) %}

   1. Select the preferred [broadcast](../../concepts/streams.md#streams) stream type:

      * `{{ ui-key.yacloud_video.streams.label_type-on-demand }}`: Start and end the broadcast manually from the {{ video-name }} interface.
      * `{{ ui-key.yacloud_video.streams.label_type-schedule }}`: Start and end the broadcast automatically at the specified time.

   1. If you selected the `{{ ui-key.yacloud_video.streams.label_type-schedule }}` stream type, specify the start and end date and time of the broadcast.
   1. (Optional) To place part of the broadcast on the website, select it as a separate episode:

      1. Click ![image](../../../_assets/console-icons/plus.svg) **{{ ui-key.yacloud_video.streams.action_add-stream-episode }}**.
      1. Enter a name and description for the episode.
      1. Specify the start and end date and time of the episode.
      1. In the **{{ ui-key.yacloud_video.thumbnails.label_thumbnail }}** field, click ![image](../../../_assets/console-icons/cloud-arrow-up-in.svg) **Select file** and select an image for the cover.

         {% include [image-characteristic](../../../_includes/video/image-characteristic.md) %}

      You can add any number of episodes. To delete an episode you do not need, click ![image](../../../_assets/console-icons/trash-bin.svg).

   1. Click **{{ ui-key.yacloud_video.common.action_create }}**.

- API {#api}

   Use the [StreamService/Create](../../api-ref/grpc/Stream/create.md) gRPC API call.

{% endlist %}