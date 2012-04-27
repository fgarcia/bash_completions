#!bash
#
# This is a reduced VBoxManage completion listing
# For a better implemention have a look at:
#
# https://github.com/tfmalt/bash-completion-virtualbox/blob/master/vboxmanage_completion.bash
#

__vboxmanage_startvm() {
    all_machines=$(VBoxManage list vms | cut -f2 -d\")
    COMPREPLY=( $(compgen -W "${all_machines}" -- ${cur}) )
}

__vboxmanage_controlvm() {
    active_machines=$(VBoxManage list runningvms | cut -f2 -d\")
    COMPREPLY=( $(compgen -W "${active_machines}" -- ${cur}) )
}


_VBoxManageCommands() {
    local cur prev command
    COMPREPLY=()
    cur="${COMP_WORDS[COMP_CWORD]}"
    prev="${COMP_WORDS[COMP_CWORD-1]}"

    command=$(set | grep ^__vboxmanage_ | sed 's/__vboxmanage_\(.*\) ()/\1/')

    case "${COMP_CWORD}" in
	1)
            COMPREPLY=( $(compgen -W "${command}" -- ${cur}) )
            ;;	
	2) 
	    if [[ $command =~ $prev ]]; then
	        __vboxmanage_$prev	
	    fi
            ;;	
	3)
	    case "${COMP_WORDS[1]}" in
		controlvm)
		    COMPREPLY=( $(compgen -W "savestate reset poweroff" -- ${cur}) )
		    return 0
		    ;;
	    esac
	    ;;
    esac
    return 0

}
complete -F _VBoxManageCommands VBoxManage

