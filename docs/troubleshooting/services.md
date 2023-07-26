# Troubleshooting Servces

## List Processes and Ports

```sh
sudo ss -lptn | column -t
```

## Get the Proceess Listening on a Port:

```sh
sudo ss -lptn 'sport = :<port>'
sudo ss -lptn | grep <port>
```

## Get a Process Enironment Variables

```sh
sudo strings /proc/<pid>/environ
```
