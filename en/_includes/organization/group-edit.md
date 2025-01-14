{% list tabs group=instructions %}

- {{ org-name }} interface {#cloud-org}

  1. [Log in]({{ link-passport-login }}) as the organization administrator.
  1. Go to [{{ org-full-name }}]({{ link-org-main }}).
  1. In the left-hand panel, select **{{ ui-key.yacloud_org.pages.groups }}** ![icon-services](../../_assets/console-icons/persons.svg).
  1. Select a [group](../../organization/concepts/groups.md) from the list and click ![image](../../_assets/console-icons/ellipsis.svg) next to the group name.
  1. Click **{{ ui-key.yacloud_org.entity.group.action_edit }}** and enter a new group name or description.

      The name must be unique within the organization and satisfy the relevant requirements:

      {% include [group-name-format](group-name-format.md) %}

  1. Click **{{ ui-key.yacloud_org.actions.save-changes }}**.

- CLI {#cli}

  {% include [cli-install](../../_includes/cli-install.md) %}

  {% include [default-catalogue](../../_includes/default-catalogue.md) %}

  1. View a description of the command to edit a {{ org-name }} user group:

      ```bash
      yc organization-manager group update --help
      ```

  1. To edit a user group, run this command:

      ```bash
      yc organization-manager group update \
        --name <group_name> \
        --new-name <new_name_for_group> \
        --organization-id <organization_ID> \
        --description <group_description>
      ```

      Where:

      * `--name`: User group name. This is a required parameter. The name must be unique within the organization and satisfy the relevant requirements:

        {% include [group-name-format](group-name-format.md) %}

      * `--new-name`: New name for the user group.
      * `--organization-id`: Organization ID. This is an optional parameter.
      * `--description`: Text description of the user group. This is an optional parameter.

- {{ TF }} {#tf}

  {% include [terraform-definition](../../_tutorials/_tutorials_includes/terraform-definition.md) %}

  {% include [terraform-install](../../_includes/terraform-install.md) %}

  1. In the configuration file, edit the group parameters:

     ```hcl
     resource "yandex_organizationmanager_group" "my-group" {
        name            = "<group_name>"
        description     = "<group_description>"
        organization_id = "<organization_ID>"
     }
     ```

     Where:

     * `name`: New group name. The name must be unique within the organization and satisfy the relevant requirements:

        {% include [group-name-format](group-name-format.md) %}

     * `description`: New group description.
     * `organization_id`: ID of the organization the group belongs to.
  1. Create resources:

     {% include [terraform-validate-plan-apply](../../_tutorials/_tutorials_includes/terraform-validate-plan-apply.md) %}

     {{ TF }} will create all the required resources. You can check the new resources and their configuration using the [management console]({{ link-console-main }}) or this [CLI](../../cli/) command:

     ```bash
     yc organization-manager group get \
       --name <group_name> \
       --organization-id <organization_ID>
     ```

- API {#api}

    Use the [Group.update](../../organization/api-ref/Group/update.md) REST API method for the [Group](../../organization/api-ref/Group/index.md) resource or the [GroupService/Update](../../organization/api-ref/grpc/Group/update.md) gRPC API call.

{% endlist %}