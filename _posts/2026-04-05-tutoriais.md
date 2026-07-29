---
title: "Tutoriais" 
date: 2026-04-05 17:20:00 -0300
categories: [Desenvolvimento de Software Livre, Tutoriais]
tags: [linux,vm,kernel]    
description: Relato sobre a fase inicial em MAC0470 
toc: false
comments: false
last_modified_at: false
---

## Tutorial 1

[Setting up a test environment for Linux Kernel Dev using QEMU and libvirt](https://flusp.ime.usp.br/kernel/qemu-libvirt-setup/)

A proposta do tutorial era ensinar como construir um ambiente de testes para desenvolvimento no kernel Linux, usando `QEMU` e `libvirt` para auxiliar na configuração de uma VM que será usada durante o processo de contribuição.

Enfrentei um pequeno problema na hora de baixar a imagem do sistema (o link do tutorial apontava para uma imagem antiga), mas foi só baxar uma imagem mais recente e tudo fluiu. Foi fácil seguir o tutorial, não enfrentei outro problema. 

## Tutorial 2

[Building and booting a custom Linux kernel for ARM using kw](https://flusp.ime.usp.br/kernel/build-linux-for-arm-kw/)

Esse tutorial ensina como construir e configurar um kernel para a arquitetura AMR.

Eu utilizei o kw e não enfreitei nenhum problema, felizmente. A compilação durou bastante (cerca de 25 minutos), mas deu tudo certo no final!

## Tutorial 3

[Introduction to Linux kernel build configuration and modules](https://flusp.ime.usp.br/kernel/modules-intro/)

O tutorial 3 ensinou como criar e carregar módulos, bem como a configurar o kernel para que ele os reconheça.

Seguindo o tutorial, implementei um driver de caractere de forma fluida, estruturando o código nos diretórios do kernel, configurando o `Kconfig` e o `Makefile`, e habilitando a compilação via `menuconfig`. Após gerar e transferir o módulo para a máquina virtual, atualizei as dependências com `depmod -a`. O único ajuste necessário ocorreu ao carregar o dispositivo via `modprobe`, pois o nó em `/dev` exigiu uma rápida correção de permissões no `udev`. 

## Tutorial 4

[Introduction to Linux kernel Character Device Drivers](https://flusp.ime.usp.br/kernel/char-drivers-intro/)

Este tutorial nos ajuda a entender o que são *Character Devices* no sistema operacional Linux e como eles funcionam. 

Criei um driver simples (simple_char.c), compilei o kernel com esse driver como módulo, o carregamos e o testamos escrevendo 256 bytes nele através de um executável que desenvolvemos. Os processos envolvidos no tutorial atual tiveram o objetivo de mostrar como os conceitos apresentados se aplicam na prática, já que escrevemos o driver com manipuladores (handlers) para syscalls e para a criação do objeto de dispositivo de caractere (cdev). Não tive nenhuma grande dificuldade neste tutorial.

## Tutoriais 5 e 6 

[Sending patches by email with git](https://flusp.ime.usp.br/git/sending-patches-by-email-with-git/) e [Sending patches with git and a USP email](https://flusp.ime.usp.br/git/sending-patches-with-git-and-a-usp-email/)

Estes dois tutoriais são mais voltados para a configuração necessária para o envio de contribuições ao kernel. 

Embora o Tutorial 5 tenha sido essencialmente conceitual sobre a estrutura do `git send-email`, o Tutorial 6 exigiu a prática de contornar as restrições de segurança do e-mail da USP via OAuth 2.0. Para isso, foi necessário configurar um proxy de e-mail e integrar o `kw` para viabilizar o envio de *patches* sem grandes percalços.

## Tutoriais 7 e 8

[The iio_simple_dummy Anatomy](https://flusp.ime.usp.br/iio/iio-dummy-anatomy/) e [IIO Dummy module Experiment One: Play with iio_dummy](https://flusp.ime.usp.br/iio/experiment-one-iio-dummy/)

O tutorial 7 ensina a criar um *Device driver* para o subsistema IIO passo a passo. Ele mostra como estruturar os canais de dados do sensor, como ler as suas medições e alterar as suas configurações. No fim, tudo se conecta na função de inicialização, que prepara a memória, ajusta as propriedades necessárias e deixa o dispositivo pronto para rodar no sistema.

No tutorial 8, o processo começou com a configuração do módulo pelo `nconfig` e o gerenciamento dos dispositivos via `configfs`, garantindo que o ambiente ficasse limpo antes do descarregamento. Em seguida, o código foi atualizado para dar suporte a uma bússola, o que envolveu definir novos canais, organizar seus índices e adaptar a função de leitura para processar o novo sensor. 

Com tudo recompilado e instalado, o driver funcionou perfeitamente nos testes.
