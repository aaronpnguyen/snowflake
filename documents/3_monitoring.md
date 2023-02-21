# Querying and Monitoring

## Access Control

1. Users are created
2. Roles are assigned to users
    - Permissions are assigned to roles
    - Roles can be assigned other roles

## Role Activation
- Users can temporarily assume the permissions of any of their roles when necessary
    - This can be done within the web portal or by using the `USE ROLE` command with SnowSQL implementation
    - Scenario: A user may be assigned both a higher and lower privileged role with the lower role being the default

## Built-in Roles
- ACCOUNTADMIN **(Most privileged role)**
    - Users with this role are able to modify almost anything within the account
- SECURITYADMIN
    - Users with this role are able to manage, monitor, and modify user roles/sessions
- SYSADMIN
    - Users with this role are able to manage, monitor, and modify account objects such as virtual warehouses, databases, and objects within databases
- USERADMIN
    - Users with this role are able to create users and roles
- PUBLIC
    - This role is granted automatically to all users within the account
> **Danger**  
> Do not grant privileges to the `PUBLIC` role directly. Best practice is to create a custom role that is then assigned to the `PUBLIC` role.
> For more information on roles, please refer to [Snowflake's documentation](https://docs.snowflake.com/en/user-guide/security-access-control-overview)

## Securables
- Snowflake offers different categories of objects that are controllables such as:
    - Databases
        - Schemas
            - Functions
            - Tables
            - Views
    - Integrations
    - Users
    - Virtual warehouses