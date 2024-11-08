# CTF5

 - Yes there is a file that is opened by the program named rules.txt.

 - Modificando o apontador fun novamente para a função readtxt podemos inserir código para ser executado

 -existe uma possibilidade de buffer-overflow já que o buffer criado é de 32 bytes e ao fazer scanf dá abertura para ler 45 caracteres de uma string ou seja 45 bytes.

 Ao sabermos disto é possível provocar um buffer-overflow de maneira a redirecionar o pointer fun para a função readtxt.

 Para realizar este exploit criámos um script em python onde chamamos o programa, criamos um payload e colocamos no scanf do programa

 Foi necessário encontrar o endereço de memória onde a função readtxt se encontra que era 0x80497a5

 sabendo isto apenas precisamos de saber o tamanho do buffer que neste caso é 32

 finalmente no payload precisamos de incluir o nome do ficheiro que pretendemos ler neste caso flag

 Assim criamos o payload da seguinte forma: b"flag\x00" + b"A" * (31 - len("flag")) + p32(0x80497a5)
 passamos \x00 depois do flag para a função sprintf presente no readtxt apenas ler o payload até este momento e ignorar o resto
 colocamos 31 - len("flag") pois é o tamanho do buffer menos tamanho da string ("flag" + "\x00")
 Fazemos p32(readtxt_address) pois o sistema que estamos a trabalhar utiliza little endian para ler endereços de memória.
