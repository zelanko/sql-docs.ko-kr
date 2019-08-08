---
ms.openlocfilehash: d2519b1cc56081f8a35308ac41e11f46a7f97211
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68215616"
---
1. **모든 SQL Server에서 Pacemaker를 위한 서버 로그인을 만듭니다**. 다음 Transact-SQL이 로그인을 만듭니다.

   ```Transact-SQL
   USE [master]
   GO
   CREATE LOGIN [pacemakerLogin] with PASSWORD= N'ComplexP@$$w0rd!'
    
   ALTER SERVER ROLE [sysadmin] ADD MEMBER [pacemakerLogin]
   ```

  가용성 그룹을 만든 이후, 노드를 추가하기 전에 pacemaker 사용자는 가용성 그룹에 대해 ALTER, CONTROL 및 VIEW DEFINITION 권한이 필요합니다.

1. **모든 SQL Server에서 SQL Server 로그인을 위한 자격 증명을 저장합니다**.

   ```bash
   echo 'pacemakerLogin' >> ~/pacemaker-passwd
   echo 'ComplexP@$$w0rd!' >> ~/pacemaker-passwd
   sudo mv ~/pacemaker-passwd /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd
   sudo chmod 400 /var/opt/mssql/secrets/passwd # Only readable by root
   ```
