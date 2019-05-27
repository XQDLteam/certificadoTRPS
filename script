#!/bin/bash 
#openssl dgst -sha1 -hmac "key" certificado-Nome1\ sobrenome-2.pdf

if [ $# -lt 1 ]; then
	echo "Faltam argumentos!"
	echo "Use: ./script <arquivo.csv>"
	exit 1
fi

input="$*"

while IFS=';' read -r line
do
	IFS=';' read -ra INFO <<< "$line"
	IFS=' ' read -ra NOME2 <<< "${INFO[1]}"
	
	file_name='certificado-'${INFO[0]}${NOME2[-1]}'.html'
	cp template_certificado.html $file_name
	sed -i "s/NOME_COMPLETO/${INFO[0]} ${NOME2[-1]}/" $file_name
	sed -i "s/CPF/${INFO[2]}/" $file_name
	
	wkhtmltopdf $file_name certificado-"${INFO[0]}-${NOME2[-1]}".pdf
	rm $file_name
	openssl dgst -sha1 -hmac "${NOME2[-1]}" certificado-"${INFO[0]}-${NOME2[-1]}".pdf 

#	echo "NOME: ${INFO[0]} ${NOME2[-1]} E-MAIL: ${INFO[2]}"

done < "$input"


