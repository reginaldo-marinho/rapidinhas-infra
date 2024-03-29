# Rapidinhas

<div style="padding: 20px; background-color: #ffc107; border-radius: 5px; box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);">
  <p><strong>Cuidado!</strong> Esse Documento é Apenas um Rascunho.</p>
</div>


## Introdução
Desenvolver aplicativos profissionais em quaisquer que sejam as tecnologias, requerem certamente pelo menos dois ambientes, `development` e `production`. Enquanto um tem foco principal nos detalhes do desenvolvimento, trazendo informações mais detalhas sobre a pilha de recursos que fazem parte do sistema como um todo o outro tem foco principal em fornecer o melhor da segurança, velocidade e simplicidade nos seus eventos internos.    

## Configuração de Ambiente

- Os ambientes no aspnet podem ser alternados atravéz das variáveis de ambiente `ASPNETCORE_ENVIRONMENT` ou `DOTNET_ENVIRONMENT`
    - Existe precedencia entre `ASPNETCORE_ENVIRONMENT` e `DOTNET_ENVIRONMENT`. **É importante saber qual tem prioridade com base no projeto desenvolvido**
    - Para ambas `launchSettings.json` define o valor `development` como padrão
    - Produção (`production`) só é aplicado quando  `ASPNETCORE_ENVIRONMENT` ou `DOTNET_ENVIRONMENT` não é definidas
    - Definir variáveis
        - No processo
            ```shell
            # Cada tipo de console tem uma sintaxe diferente
            set ASPNETCORE_ENVIRONMENT=Staging
            dotnet run --no-launch-profile
            ```
        - Definir variáveis Globalmente
            - [Windows](https://www.oobj.com.br/bc/article/como-configurar-variavel-de-ambiente-no-windows-para-emiss%C3%A3o-de-mf-e-1180.html)
            - Linux
        - Definir variáveis Configs
            - [web.config](https://learn.microsoft.com/pt-br/aspnet/core/host-and-deploy/iis/web-config?view=aspnetcore-8.0#set-environment-variables)
            - [IIS](https://learn.microsoft.com/pt-br/aspnet/core/host-and-deploy/visual-studio-publish-profiles?view=aspnetcore-8.0)
    
- `Properties/launchSettings.json`
    - **Define diferentes perfis**
        - Podemos escolhar o perfil pela cli `dotnet run --launch-profile "MeuPperfil"`

    - Deve ser usado apenas no cumputador local
    - Não é implantado.
    - As variavies de ambiente definidas aqui substituem as definidas pelo sistema
    - **Não guarde segredos|senhas nesse aquivo**
- `Properties/PublishProfiles` são opções usadas na publicação do projeto


- `.vscode/launch.json`
    - É uma alternativa para  `Properties/launchSettings.json`? **Estudar**
- Para mudar o ambiente via linha de comando usamos
    - `dotnet run --environment Production`

## Strings de Conexão
- Criptografia
- Devem sempre vir de algum arquivo de configuração, e mesmo assim não deve ter dados confidenciais expostos
- Não deixar senhas e se possível o nome do banco de dados esposto

## Secrets Manager


## Sobre ambientes de Produção

- Deve Maximizar a segurança, o desempenho e a robustez do aplicativo
    - Frontend
        - Minificadores -  `min.css`, `min.js`
        - Empacotadores
        - Servidos via CDN

- Memoria
    - Cache
    - Páginas de erro
        - Diagnóstico desabilitadas.
        - Paginas Amigáveis habilitadas.
    - Log
        - Monitoramento de produção habilitados
        - Logs (Que fazem sentido)

## Publicar o APP

- CLI `dotnet publish`
    - Compila o Projeto e publica o resultado
    - Arquivos de saida
        - .dll
        - .deps.json
        - .runtimeconfig.json 
    - Sua saida pode ser  usada por sistemas de hospedagem
        - apache
        - iis
        - nginx
    - [Referencia](https://learn.microsoft.com/pt-br/dotnet/core/tools/dotnet-publish)
     
    
- inetpub
    - É a pasta padrão do Microsoft Internet Information Services (IIS)
    - Fornece informações de Logs 
    - Fornece sites em wwwroot
        - **Se o site informado estiver fora da pasta `ìnetpub`, possivelmente terá erros de permissções, fique atento!**
    - entre  outras coisas 
