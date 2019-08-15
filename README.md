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
Your daily dose of nectar according to the sweet will of Sri Guru Maharaja. Inspired by a devotee on Reddit who loves Govinda. :)

I used bash, grep and awk to generate the selections. The code is not pretty but it works!

Themes (tags) can be requested. You can also search your own sweetness using the Random page.

Contact me on Reddit or Discord, *soul4krsna* or *bhagavatam.purana@gmail.com*

**Jaya Sri Prabhupada! Jaya Nitai-Gaur! Jaya Radha-Krsna!**

```bash
a1 () {
    awk '{print $1}'
}

a2 () {
    awk '{print $2}'
}

a3 () {
    awk '{print $3}'
}

gita=/krsna/home/krsna-online/sites/rand-serv/gita
gita-rand () {
	grep -w "$1" "$gita" | a1 | cat -n > bgloc
	end=$(tail -1 bgloc | a1)
	random=$(awk -v min=1 -v max=$end 'BEGIN{srand();\
	      print int(min+rand()*(max-min+1))}')
	line=$(grep -w $random bgloc | a2)
	bgverse=$(grep -w -B50 "$line" "$gita" | grep '###'\
	     | tail -1| a3 | tr '.' ' '\
	     | awk '{ print "cp /krsna/home/krsna-online/gita/isrc/"$1"/src/"$2".md"}')
	eval $bgverse "."
	echo "gita:"$1"= nectar $random of $end" >> selection-bg
	cat selection-bg 

}

sb=/krsna/home/krsna-online/sites/rand-serv/sb
sb-rand () {
	grep -w "$1" "$sb" | a1 | cat -n > sbloc
        end=$(tail -1 sbloc | a1)
        random=$(awk -v min=1 -v max=$end 'BEGIN{srand();\
              print int(min+rand()*(max-min+1))}')
        line=$(grep -w $random sbloc | a2)
	sbverse=$(grep -w -B50 "$line" "$sb" | grep '###'\
	       | tail -1 | a3)
	find /krsna/home/krsna-online/bhagavatam/isrc\
	-name $(echo "$sbverse".md) -exec cp {} "." \; 
        echo "sb:"$1"= nectar $random of $end" >> selection-sb
	cat selection-sb 
}

nr () {
	gita-rand "$1"
	sb-rand "$1"
}

```

