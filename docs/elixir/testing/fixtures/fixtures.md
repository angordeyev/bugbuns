# Text Fixtures

## General

Fixtures is a known state against which a test is running, an object with test data.

Example

    ➜ mix phx.gen.context Communication Message messages text:string

    defmodule HelloTesting.CommunicationFixtures do
      @moduledoc """
      This module defines test helpers for creating
      entities via the `HelloTesting.Communication` context.
      """

      @doc """
      Generate a message.
      """
      def message_fixture(attrs \\ %{}) do
        {:ok, message} =
          attrs
          |> Enum.into(%{
            text: "some text"
          })
          |> HelloTesting.Communication.create_message()

        message
      end
    end

    ➜ iex -S mix test

## Ecto Fixtures

The autogenerated fixtures looks like this

    defmodule HelloAssoc.BlogFixtures do
      @moduledoc """
      This module defines test helpers for creating
      entities via the `HelloAssoc.Blog` context.
      """

      @doc """
      Generate a post.
      """
      def post_fixture(attrs \\ %{}) do
        {:ok, post} =
          attrs
          |> Enum.into(%{
            text: "some text"
          })
          |> HelloAssoc.Blog.create_post()

        post
      end

      @doc """
      Generate a comment.
      """
      def comment_fixture(attrs \\ %{}) do
        {:ok, comment} =
          attrs
          |> Enum.into(%{
            text: "some text"
          })
          |> HelloAssoc.Blog.create_comment()

        comment
      end
    end

Using assoc

[Fixtures for Ecto](https://blog.danielberkompas.com/2015/07/16/fixtures-for-ecto/)

## Resources

[^2]: test fixture - испытательный стенд