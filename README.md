# Minecraft Server Docker Image

A production-ready Docker image for running a Minecraft Paper server with built-in Samba file sharing and MySQL database support.

## Features

- **Paper Minecraft Server**: Latest Paper 1.21.4 server for optimal performance
- **Samba File Sharing**: Built-in SMB server for easy world file access
- **MySQL Database**: Integrated MySQL server for plugins requiring database support
- **Supervisor Management**: Uses supervisord to manage all services
- **Log Rotation**: Automatic log rotation to prevent disk space issues
- **Docker Swarm Ready**: Optimized configuration for both standalone and swarm deployments

## Quick Start

```bash
docker-compose up -d
```

Access your Minecraft server at port 25565 and connect to the Samba share at `\\your-server-ip\minecraft`.

## Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| MYSQL_USER | MySQL username | mcuser |
| MYSQL_PASSWORD | MySQL password | *random if not specified* |
| MYSQL_DATABASE | MySQL database name | minecraft |
| SMB_USER | Samba username | mcadmin |
| SMB_PASSWORD | Samba password | *random if not specified* |
| TZ | Timezone | UTC |

## Ports

- **25565**: Minecraft server
- **25575**: RCON port
- **3306**: MySQL
- **445/139**: SMB/CIFS
- **137/138**: NetBIOS (UDP)

## Volumes

- **/minecraft**: Game server files
- **/var/lib/mysql**: MySQL database
- **/var/log/samba**: Samba logs
- **/var/log/supervisor**: Supervisor logs

## Advanced Configuration

### Custom Server Properties

Mount your `server.properties` file to `/minecraft/server.properties`.

### Custom Samba Config

To customize Samba, modify and mount your own `smb.conf` file.

### Java Memory Settings

Modify the Java memory settings in supervisord.conf to adjust server performance:

```
-Xms6G -Xmx6G
```

## Security Notes

- Always change default passwords in production environments
- Consider using Docker secrets for credentials in Swarm mode
- The container runs services as root for simplicity - consider custom security settings for production

## Swarm Deployment

A `docker-compose-swarm.yml` file is included for Docker Swarm deployments.

## License

See the [LICENSE](LICENSE) file for details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.