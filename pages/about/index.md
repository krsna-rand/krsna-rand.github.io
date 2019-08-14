<!--
.. title: About
.. slug: about
.. date: 2019-08-12 16:30:51 UTC-04:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->

Your daily dose of nectar according to the sweet will of Sri Guru Maharaja.
Inspired by a devotee on Reddit who loves Govinda. :) 

I used *bash, grep and awk* to generate the selections.
The code is not pretty but it works!

Themes (tags) can be requested.
**Contact:** __Reddit__ or __Discord__ *soul4krsna*

**Jaya Sri Prabhuda! Jaya Nitai! Jaya Krsna!**

```bash

a1 () {
    awk '{print $1}'
}

a2 () {
    awk '{print $2}'
}

gita=/krsna/home/krsna-online/sites/rand-serv/gita
gr () {
    grep "$1" "$gita" | a1 | cat -n > bgloc
    end=`grep "$1" "$gita" | a1 | cat -n | a1 | tail -1`
    post=`awk -v min=1 -v max=$end 'BEGIN{srand(); print int(min+rand()*(max-min+1))}'`
    grep -w "$post" bgloc
    echo "gita:"$1"= nectar $post of $end" >> selection-bg 

}

rbgv () {
    line=`gr "$1" | a2`
    grep -B50 "$line" "$gita" | grep '###' | tail -1 | awk '{ print $3 }' | tr '.' ' '> tbgv
    `cat tbgv | awk '{ print "cp /krsna/home/krsna-online/gita/isrc/"$1"/src/"$2".md"}'` "$PWD/"
     mv "$(cat tbgv | a2).md" "$(echo `cat tbgv | tr ' ' '.'`.md)"
     cat selection-bg
     cat tbgv >> hist-bg
}

sb=/krsna/home/krsna-online/sites/rand-serv/sb
sb () {
    grep "$1" "$sb" | a1 | cat -n >> sbloc
    end=`grep "$1" "$sb" | a1 | cat -n | a1 | tail -1`
    post=`awk -v min=1 -v max=$end 'BEGIN{srand(); print int(min+rand()*(max-min+1))}'`
    grep -w "$post" sbloc
    echo "bhagavatam:"$1"= nectar $post of $end" >> selection-sb

}

rsbv () {
    line=`sb "$1"  | a2`
    grep -B50 "$line" "$sb" | grep '###' | tail -1 | awk '{ print $3 }' > tsbv
    find /krsna/home/krsna-online/bhagavatam/isrc -name $(echo `cat tsbv`.md) -exec cp {} $PWD \; 
    cat selection-sb ; cat tsbv >> hist-sb ; cat tsbv
}

nr () {
	rbgv "$1"
	rsbv "$1"
}

```

