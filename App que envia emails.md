# Criando App para envio emails

### Aqui apresenta uma simples aplicação:

![image](https://github.com/jacimarajp/python/assets/24573177/fe950ee6-48d1-40cc-b651-7c8debe414bc)



```
"""programa envia emails para qualque pessoa

@author: Jacimara

"""
from tkinter import messagebox, Tk, Label, Entry, Button

from string import Template
#importe a biblioteca do smtp: protocolo de envio de emails
import smtplib
# import necessary packages
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
#Lê os email no arquivo my_contacts e retorna uma lista de endereços de emails


def get_contacts(filename):
    names = []
    emails = []
    with open (filename, mode='r', encoding='utf-8') as contacts_file:
        for a_contact in contacts_file:
            names.append(a_contact.split()[0])
            emails.append(a_contact.split()[1])
    return names, emails


def gera_email():

    texto_da_mensagem = website_entry.get()
    emails = str(website_entry2.get())

    # set o servidor smtp
    s = smtplib.SMTP(host='smtp.office365.com', port=587)
    s.starttls()
    # use o email e senha que vai ser usado para enviar emails
    s.login('jacimara196@hotmail.com', 'vitoria31101997')
    message_template = str(texto_da_mensagem)
    emails = emails.split()
    # For each contact, send the email
    for email in emails:
        msg = MIMEMultipart()  # cria a mensagem

        # adiciona na mensagem o nome da pessoa,escrito no arquivo my_contacts
        message = message_template

        # Configuração dos paramentros da mensagem
        msg['from'] = 'jacimara196@hotmail.com'
        msg['to'] = email
        msg['Subject'] = "This is Test"

        # Adicione ao corpo da mensagem
        msg.attach(MIMEText(message, 'plain'))

        # envia a mensagem
        s.send_message(msg)

        del msg


if __name__ == '__main__':

    window = Tk()
    window.title("App de enviar Emails")
    window.config(padx=10, pady=100, background='#BFDDF3')

    # Labels
    website_label = Label(text="EMAIL:")
    website_label.grid(row=1, column=0)

    # Labels
    website_label2 = Label(text="ADDRESS:")
    website_label2.grid(row=0, column=0)

    # Entries
    #website_entry campo que irá receber a url e a função de gera qr code irá pegar
    website_entry = Entry(width=35)
    website_entry.grid(row=1, column=1, columnspan=2)
    #website_entry.place(relx = 0.1, rely = 0.1,relwidth = 0.8, relheight=2)
    website_entry.focus()

    # Entries
    #website_entry campo que irá receber o email para enviar
    website_entry2 = Entry(width=35)
    website_entry2.grid(row=0, column=1, columnspan=2)
    #website_entry.place(relx = 0.1, rely = 0.1,relwidth = 0.8, relheight=2)
    website_entry2.focus()

    add_button = Button(text="Enviar Email", width=10, command=gera_email)
    add_button.grid(row=4, column=2, columnspan=2)

    window.mainloop()
```
Referências:

https://www.freecodecamp.org/portuguese/news/enviar-emails-usando-python/

https://pythonacademy.com.br/blog/interfaces-graficas-com-tkinter-e-python#instala%C3%A7%C3%A3o-das-depend%C3%AAncias
