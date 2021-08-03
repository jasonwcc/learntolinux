# Bash autocompletion for other commands

vi ~/.bashrc
alias kc=kubectl
alias docker=podman

source <(kubectl completion bash)
source <(helm completion bash)

complete -F __start_kubectl kc

# Bash autocompletion for git command
curl https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash -o /etc/bash_completion.d/git

t 
