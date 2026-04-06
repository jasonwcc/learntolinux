```
\u		# hostname
\t		# time
\d		# date
\n		# newline
\w or \W
\e[30m		black
\e[31m		red
\e[32m		green
\e[33m		yellow
\e[34m		blue
\e[35m		magenta
\e[36m		cyan
\e[37m		white
\[ 		start of non-printing sequence
\]		end of non-printing sequence

PS1="\[\033[1;32m\]\d\[\033[m\] | \[\033[1;35m\]\t\[\033[m\] | \[\033[m\]\[\e[0m\]\[\e[1;36m\][\w] \[\e[1;32m\]\n\u@\h> "

Show fancy emoticon if exit code is non-zero (applicable only with putty and mac terminal)
PS1="\`if [ \$? = 0 ]; then echo 👍 ; else echo 🔥; fi\`\[\e[35m\] [\u@\h] \[\e[30m\]:\[\e[36m\]\`if [ \$? = 0 ]; then echo 🌈; else echo 🔥; fi\` \w\[\e[37m\] $ "
PS1=" \`if [ \$? = 0 ]; then echo 👍 ; else echo 🔥; fi\`\[\e[35m\] [\u@\h] \[\e[30m\]:\[\e[36m\] 🌈 \w\[\e[37m\] $ "
PS1="\[\033[1;37m\]\d\[\033[m\] | \[\033[1;35m\]\t\[\033[m\] | \[\033[m\]\[\e[0m\]\[\e[1;32m\][\w] \n\[\e[0m\]\`if [ \$? = 0 ]; then echo 👍 ; else echo 🔥; fi\` \[\e[1;33m\]\u\[\e[1;36m\]\[\033[m\]@\[\e[1;36m\]\h \[\e[0m\] > "
PS1="\[\033[1;37m\]\d\[\033[m\] | \[\033[1;35m\]\t\[\033[m\] | \[\033[m\]\[\e[0m\]\[\e[1;32m\][\w] \n\[\e[0m\]\`if [ \$? = 0 ]; then echo 👍 ; else echo 🔥; fi\` \[\e[1;33m\]\u\[\e[1;36m\]\[\033[m\]@\[\e[1;36m\]\h 🌈 \[\e[0m\] > "

```
