# Sistema de Arquivos
O sistema de arquivos usado nas versões modernas do Windows é o New Technology File System ou NTFS.

Antes do NTFS, havia o FAT16/FAT32 (File Allocation Table) e o HPFS (High Performance File System).

Você ainda vê partições FAT em uso hoje. Por exemplo, normalmente você vê partições FAT em dispositivos USB, cartões MicroSD, etc., mas tradicionalmente não em computadores/laptops pessoais com Windows ou servidores Windows.

O NTFS é conhecido como um sistema de arquivos com registro em diário. Em caso de falha, o sistema de arquivos pode reparar automaticamente as pastas/arquivos no disco usando as informações armazenadas em um arquivo de log. Essa função não é possível com o FAT.

O NTFS aborda muitas das limitações dos sistemas de arquivos anteriores, como:

* Suporta arquivos maiores que 4 GB
* Definir permissões específicas para pastas e arquivos
* Compactação de pastas e arquivos
* Criptografia ([Encryption File System](https://learn.microsoft.com/en-us/windows/win32/fileio/file-encryption) ou EFS)
