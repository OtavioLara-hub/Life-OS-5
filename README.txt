LIFEOS 4.0 — CONFIGURAÇÃO E MIGRAÇÃO

O que está preparado:
- Interface LifeOS 3.1 preservada como base.
- Tela de login e criação de conta por e-mail/senha.
- Estrutura Supabase para dados privados por usuário (RLS).
- Migração automática: se a conta ainda não tiver dados na nuvem, os dados locais deste navegador são enviados no primeiro login.
- Atualizações Realtime para alterações recebidas de outro dispositivo.
- PWA instalável e service worker para cache do app shell.

PASSO A PASSO
1. Crie um projeto gratuito em https://supabase.com/.
2. No SQL Editor do Supabase, execute todo o conteúdo de supabase.sql.
3. Em Project Settings > API, copie Project URL e anon/public key.
4. Cole os dois valores em config.js. NUNCA use service_role key no navegador.
5. Em Database > Publications, habilite Realtime para public.lifeos_user_data.
6. Hospede a pasta inteira em um host estático HTTPS (ex.: GitHub Pages ou Cloudflare Pages).
7. Abra o endereço hospedado no PC, crie a conta e entre.
8. No primeiro login, se a tabela ainda não tiver dados para essa conta, os dados locais desse navegador serão migrados para a nuvem.
9. No celular, abra o mesmo endereço e entre com a mesma conta.

MIGRAÇÃO DOS DADOS 3.1
- Antes de começar, exporte um backup pelo LifeOS 3.1.
- O primeiro login importa automaticamente a chave local lifeos_v1_data do navegador usado.
- Se seus dados do LifeOS 3.1 estão em outro navegador/dispositivo, primeiro importe o backup 3.1 nesse navegador antes de fazer o primeiro login.
- Se já existir uma linha na nuvem para a conta, os dados da nuvem prevalecem. Faça backup antes de substituir qualquer coisa.

LIMITAÇÕES IMPORTANTES DESTA BASE 4.0
- O pacote é uma base implementável, mas ainda exige criar/configurar o projeto Supabase e publicar o site. Não há URL pública nem credenciais criadas por este pacote.
- O salvamento local continua como cache; se estiver offline, as alterações permanecem locais, mas esta primeira implementação ainda não tem uma fila offline robusta com resolução avançada de conflitos.
- O Realtime atual recebe eventos UPDATE de outros dispositivos. Para operações simultâneas intensas, será necessário evoluir para sincronização por registro/evento em vez de um único JSON agregado.
- A autenticação depende da confirmação de e-mail conforme as configurações do projeto Supabase.

SEGURANÇA
- Não compartilhe sua senha.
- Nunca publique a service_role key.
- A anon/public key pode ficar no front-end somente com RLS corretamente habilitado.
