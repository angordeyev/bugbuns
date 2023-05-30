## Sockets

    {:ok, socket} = :socket.open(:local, :stream)
    :ok = :socket.bind(socket, %{family: :local, path: "/tmp/demo2.sock"})
    :ok = :socket.listen(socket)
    {:ok, socket} = :socket.accept(socket)


    {ok, LSock} = socket:open(inet, stream, tcp),
    ok = socket:bind(LSock, #{family => inet,
                              port   => Port,
                              addr   => Addr}),
    ok = socket:listen(LSock),
    {ok, Sock} = socket:accept(LSock),
    {ok, Msg} = socket:recv(Sock),


## Comments

    gen_tcp used do_recv block

    https://www.erlang.org/doc/man/gen_tcp.html
