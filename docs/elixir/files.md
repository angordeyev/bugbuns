## Working with directories and files

Creating a new file with content

    iex> File.write("tmp.txt\n", "Hello file")
    :ok

    iex> File.read("tmp.txt")
    {:ok, "Hello file\n"}

    iex> File.write("tmp.txt", "Hello new\n")
    :ok

    iex> File.read("tmp.txt")
    {:ok, "Hello new\n"}

Append to file

    iex> File.write("tmp.txt", "line2\n", [:append])
    :ok

    iex> File.read("tmp.txt")

Using heredoc

    iex> File.write("tmp.txt", """
    line1
    line2
    """)

    :ok

    iex> File.read("tmp.txt")
    {:ok, "line1\nline2\n"}

    iex> IO.puts(File.read!("tmp.txt"))
    line1
    line2

    :ok

