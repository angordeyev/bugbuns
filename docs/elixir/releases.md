# Releases

## Phoenix releases

Generate release helper files for Phoenix

    ➜ mix phx.gen.release
    ➜ MIX_ENV=prod mix release

## Deploy release

Create database

    ➜ sudo -u postgres psql -c 'create database hello_phx;' # create db

Generate secret

    ➜ mix phx.gen.secret # on other machine because mix does not exist here

Create unit file

    ➜ sudo touch /etc/systemd/system/<appname>.service
    ➜ sudo chmod 644 /etc/systemd/system/<appname>.service

    [Unit]
    Description=<appname>
    # after file systems are mounted and network is available
    After=local-fs.target network.target

    [Service]
    User=webapp
    Group=webapp

    # cd to the folder
    WorkingDirectory=/srv/<appname>
    ExecStart=/srv/<appname>/bin/server
    ExecStop=/srv/<appname>/bin/<appname> stop

    # mask for default files permissions create by daemon
    UMask=027

    # the service will be restarted regardless of whether it exited cleanly or not
    Restart=always

    Environment=MIX_ENV=prod
    Environment=PORT=4001
    Environment=DATABASE_URL=ecto://postgres:postgres@localhost/<appname>
    # generate SECRET using "mix phx.gen.secret"
    Environment=SECRET_KEY_BASE=<SECRET>

    [Install]
    # common for services, starts the service when systemd loads multi-user.target
    WantedBy=multi-user.target

## Environment variables

    ➜ API_KEY="some_secret" iex

    iex> System.fetch_env!("API_KEY")
    "some_secret"

## Overlays

Files in rel/overlays are copied to the release after it is build

    ➜ mkdir -p rel/overlays; touch rel/overlays/hello_overlay.txt
    ➜ mix release

See `_build/dev/rel/hello_release/hello_overlay.txt` is created

## Diagnostics and docs

Show default unit file paramsters

    systemctl --user show syncthing | grep LimitNOFILE

### Access from other machines or web

Change binding to {0, 0, 0, 0}

    config :hello_phx, HelloPhxWeb.Endpoint,
      ...
      http: [ip: {0, 0, 0, 0}, port: 4000],
      ...

## Cross compiling

Cross compiling is compiling for another platform

[Cross compiling with Docker](https://nts.strzibny.name/cross-compiling-elixir-releases/#:~:text=Elixir%20releases%20are%20self%2Dcontained,are%20unfortunately%20not%20platform%2Dindependent.)

## Resources

[Unit file described](https://debian.pro/2602)
[Environment variables](https://mbuffa.github.io/tips/20210916-elixir-environment-variables/#:~:text=An%20environment%20variable%20is%20a,on%20that%20aspect%20for%20beginners.&text=And%20the%20same%20call%20would%20work%20in%20your%20application%20source%20code)
[Elixir releases](https://staknine.com/)
[Deployment to server](https://elixirforum.com/t/what-is-the-best-way-to-deploy-a-phoenix-application-to-ec2-or-digital-ocean/41284/3)
[Is there a typical way to pass a password to a Systemd Unit file?](https://unix.stackexchange.com/questions/391040/is-there-a-typical-way-to-pass-a-password-to-a-systemd-unit-file)
[Deploying Go Application with systemd](https://jonathanmh.com/deploying-go-apps-systemd-10-minutes-without-docker/)
[Storing secret environment variables for deamon using libsecret](https://unix.stackexchange.com/questions/391040/is-there-a-typical-way-to-pass-a-password-to-a-systemd-unit-file)
[Config and Releases](https://elixir-lang.org/getting-started/mix-otp/config-and-releases.html)
