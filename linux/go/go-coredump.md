- https://rakyll.org/coredumps/
- https://github.com/go-delve/delve/tree/master/Documentation/cli

```
root@gyliu-dev1:~/test/hello# dlv core ./hello core
Type 'help' for list of commands.
(dlv) goroutine
Thread 14351 at /usr/local/go/src/runtime/sys_linux_amd64.s:150
(dlv) bt
 0  0x0000000000459c91 in runtime.raise
    at /usr/local/go/src/runtime/sys_linux_amd64.s:150
 1  0x0000000000440e3b in runtime.dieFromSignal
    at /usr/local/go/src/runtime/signal_unix.go:424
 2  0x0000000000441298 in runtime.sigfwdgo
    at /usr/local/go/src/runtime/signal_unix.go:629
 3  0x00000000004404e0 in runtime.sigtrampgo
    at /usr/local/go/src/runtime/signal_unix.go:289
 4  0x0000000000459f83 in runtime.sigtramp
    at /usr/local/go/src/runtime/sys_linux_amd64.s:357
 5  0x00007fa7e9588390 in (nil)
    at ?:-1
 6  0x0000000000440fda in runtime.crash
    at /usr/local/go/src/runtime/signal_unix.go:518
 7  0x000000000043fd6c in runtime.sighandler
    at /usr/local/go/src/runtime/signal_sighandler.go:148
 8  0x0000000000440692 in runtime.sigtrampgo
    at /usr/local/go/src/runtime/signal_unix.go:351
 9  0x0000000000459f83 in runtime.sigtramp
    at /usr/local/go/src/runtime/sys_linux_amd64.s:357
10  0x00007fa7e9588390 in (nil)
    at ?:-1
(dlv) goroutines
[4 goroutines]
  Goroutine 1 - User: /usr/local/go/src/runtime/netpoll.go:182 internal/poll.runtime_pollWait (0x429566)
  Goroutine 2 - User: /usr/local/go/src/runtime/proc.go:302 runtime.gopark (0x42e82f)
  Goroutine 3 - User: /usr/local/go/src/runtime/proc.go:302 runtime.gopark (0x42e82f)
  Goroutine 18 - User: /usr/local/go/src/runtime/proc.go:302 runtime.gopark (0x42e82f)
(dlv) Goroutine 1
Command failed: command not available
(dlv) goroutine 1
Switched from 0 to 1 (thread 14351)
(dlv) bt
 0  0x000000000042e82f in runtime.gopark
    at /usr/local/go/src/runtime/proc.go:302
 1  0x0000000000429f6a in runtime.netpollblock
    at /usr/local/go/src/runtime/netpoll.go:389
 2  0x0000000000429566 in internal/poll.runtime_pollWait
    at /usr/local/go/src/runtime/netpoll.go:182
 3  0x00000000004a18bb in internal/poll.(*pollDesc).wait
    at /usr/local/go/src/internal/poll/fd_poll_runtime.go:87
 4  0x00000000004a2eba in internal/poll.(*pollDesc).waitRead
    at /usr/local/go/src/internal/poll/fd_poll_runtime.go:92
 5  0x00000000004a2eba in internal/poll.(*FD).Accept
    at /usr/local/go/src/internal/poll/fd_unix.go:384
 6  0x0000000000534722 in net.(*netFD).accept
    at /usr/local/go/src/net/fd_unix.go:238
 7  0x0000000000549022 in net.(*TCPListener).accept
    at /usr/local/go/src/net/tcpsock_posix.go:139
 8  0x0000000000547bc8 in net.(*TCPListener).AcceptTCP
    at /usr/local/go/src/net/tcpsock.go:247
 9  0x0000000000625d1f in net/http.tcpKeepAliveListener.Accept
    at /usr/local/go/src/net/http/server.go:3264
10  0x00000000006456ec in net/http.(*onceCloseListener).Accept
    at <autogenerated>:1
(dlv) goroutine 2
Switched from 1 to 2 (thread 14351)
(dlv) bt
0  0x000000000042e82f in runtime.gopark
   at /usr/local/go/src/runtime/proc.go:302
1  0x000000000042e6d7 in runtime.goparkunlock
   at /usr/local/go/src/runtime/proc.go:307
2  0x000000000042e6d7 in runtime.forcegchelper
   at /usr/local/go/src/runtime/proc.go:250
3  0x0000000000458381 in runtime.goexit
   at /usr/local/go/src/runtime/asm_amd64.s:1337
(dlv) ls
> runtime.gopark() /usr/local/go/src/runtime/proc.go:302 (PC: 0x42e82f)
Warning: debugging optimized function
   297:		mp.waittraceev = traceEv
   298:		mp.waittraceskip = traceskip
   299:		releasem(mp)
   300:		// can't do anything that might move the G between Ms here.
   301:		mcall(park_m)
=> 302:	}
   303:
   304:	// Puts the current goroutine into a waiting state and unlocks the lock.
   305:	// The goroutine can be made runnable again by calling goready(gp).
   306:	func goparkunlock(lock *mutex, reason waitReason, traceEv byte, traceskip int) {
   307:		gopark(parkunlock_c, unsafe.Pointer(lock), reason, traceEv, traceskip)
(dlv) p park_m
Command failed: could not find symbol value for park_m
(dlv) p mp
(unreadable could not find loclist entry at 0x3665d for address 0x42e82f)
(dlv) locals mp
mp = (unreadable could not find loclist entry at 0x3665d for address 0x42e82f)
(dlv) locals reason
(no locals)
```
