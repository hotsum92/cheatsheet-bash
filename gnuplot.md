```
gnuplot --persist -e 'plot sin(x)'
```

```
gnuplot --persist << EOF
plot sin(x)
EOF
```

```
gnuplot << EOF
set terminal png
set output "sin.png"
plot sin(x)
EOF
```

```

gnuplot << EOF
set terminal png
set output "output.png"
set style data linespoints
set datafile separator ","
set xdata time
set timefmt "%b %d %H:%M:%S GMT %Y"
set xlabel "timestamp"
set ylabel "percent"
plot "data.csv" using 1:3 title "a","data.csv" using 1:4 title "b"
EOF

```

```

gnuplot --persist << EOF
set style data linespoints
set datafile separator ","
set xdata time
set timefmt "%b %d %H:%M:%S GMT %Y"
set xlabel "timestamp"
set ylabel "percent"
plot "data.csv" using 1:3 title "A","data.csv" using 1:4 title "B"
EOF

```

```
gnuplot --persist -e 'plot for [i=2:*] "< cat -" using 1:i title columnheader(i) with linespoints'
```

```
tmpfile=$(mktemp)

cat - | awk '{print NR, $0}' > $tmpfile

gnuplot --persist -e "plot for [i=3:*] \"$tmpfile\" using 1:i:xtic(2) title columnheader(i) with linespoints" 2>/dev/null
```
