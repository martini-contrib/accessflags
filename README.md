# accessflags [![wercker status](https://app.wercker.com/status/41eabb68b7b41be396b33cd08c0b6daa/s/ "wercker status")](https://app.wercker.com/project/bykey/41eabb68b7b41be396b33cd08c0b6daa)

`accessflags` is a Martini handler to enable Access Control, such as role-based access control support, through an integer flag.

[API Reference](http://gowalker.org/martini-contrib/accessflags)

## Usage

~~~go
package main

import (
	"github.com/martini-contrib/accessflags"
	"github.com/codegangsta/martini"
)

const (
	rolePassAll = 0
	roleRobot   = 1
	roleSignOn  = 2
	roleAdmin   = 4 | roleSignOn
)

func main() {
	m := martini.Classic()

	m.Use(judge) // first Map flag for role
	m.Get("/profile", accessflags.Forbidden(roleSignOn), profileHandler)
	m.Get("/admin", accessflags.Forbidden(roleAdmin), adminHandler)

	m.Run()
}

func judge(c martini.Context) martini.Handler{
	// something
	c.Map(roleRobot) // roleSignOn...
}

func adminHandler() string{
	// something
	return "hello"
}
func profileHandler() string{
	// something
	return "profile"
}
~~~

## Authors
* [Yu HengChun](http://github.com/achun)
