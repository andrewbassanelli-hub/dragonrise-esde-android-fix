# Solução alternativa: DragonRise 0079:0006 no ES-DE Android

**Testado e documentado por Andrew Bassanelli — 8 de novembro de 2026.**

> **Escopo:** configuração testada em um único gabinete arcade Android. Não é uma correção universal, nem um patch oficial do ES-DE ou da SDL.

## Ambiente testado

- **Dispositivo:** Samsung Galaxy Tab S4
- **Sistema:** Android (versão exata não documentada neste relato)
- **Frontend:** ES-DE 3.5.0-65 (r52)
- **SDL informada no registro do ES-DE:** 2.32.10
- **Controladora USB:** DragonRise Inc. / PC TWIN SHOCK Gamepad
- **Identificador VID:PID:** `0079:0006`
- **Comandos:** joystick arcade + seis botões físicos

## Problema observado

O controle respondia no aplicativo de testes de gamepad do Android e no RetroArch, mas não era reconhecido como controle pelo ES-DE. Antes da solução, o registro de inicialização mostrava `Added keyboard with default configuration`, sem uma entrada de adição de controle.

## Arquivo de configuração testado

Baixe [`es_controller_mappings.cfg`](es_controller_mappings.cfg) ou crie um arquivo de texto com a linha abaixo:

```text
default,DragonRise Arcade Android Buttons Test,a:b20,b:b21,x:b22,y:b23,back:b24,start:b25,dpup:b11,dpdown:b12,dpleft:b13,dpright:b14,leftx:a0,lefty:a1,platform:Android,
```

**Atenção:** este mapeamento usa `default`, e não um GUID específico da controladora. Isso significa que ele pode afetar outros controles ainda não mapeados pelo SDL. Não o aplique indiscriminadamente em outros sistemas.

## Instalação

1. Feche completamente o ES-DE.
2. Localize a **pasta de dados do ES-DE** no Android (pasta `ES-DE` definida no armazenamento do aplicativo; a localização pode variar).
3. Dentro dela, abra ou crie a subpasta `controllers`.
4. Se já existir `es_controller_mappings.cfg`, faça uma cópia de segurança.
5. Coloque o arquivo fornecido em `ES-DE/controllers/es_controller_mappings.cfg`, em relação à pasta de dados do ES-DE.
6. Inicie novamente o ES-DE e teste o joystick e os seis botões na interface.
7. Se houver comportamento incorreto, feche o ES-DE, remova o arquivo de teste e restaure o original, se existia.

Não foi necessário root nem aplicativo de remapeamento rodando em segundo plano no ambiente testado.

## Resultado confirmado e limitações

**Confirmado no dispositivo testado:** o joystick e os seis botões funcionaram na interface do ES-DE depois da instalação do arquivo.

- Outros controles DragonRise podem usar o mesmo ID `0079:0006` com ligações e numeração de botões diferentes.
- Os botões Android `b20`–`b25` correspondem a esta configuração específica.
- Não houve validação em outras versões de Android, ES-DE, SDL ou outros modelos de controladora.
- O funcionamento da interface do ES-DE não garante configuração automática dos controles dentro dos jogos ou emuladores.
- Esta solução é um contorno, não uma correção definitiva no código-fonte.

## Colabore com testes

Se funcionar no seu sistema, informe dispositivo, versão do Android, versão do ES-DE/SDL, VID:PID, layout de botões/eixos e resultado. Relatos negativos também são importantes.

## Apoio voluntário

Se este tutorial ajudou, você pode [fazer uma doação voluntária pela Wise](https://wise.com/pay/me/andrewb8447). A solução é gratuita; a doação é opcional.

**Crédito:** Andrew Bassanelli — responsável pelos testes e pela documentação desta solução específica. Projeto independente, não afiliado à equipe do ES-DE ou da SDL.

**English:** [Read the English guide](README.md).
