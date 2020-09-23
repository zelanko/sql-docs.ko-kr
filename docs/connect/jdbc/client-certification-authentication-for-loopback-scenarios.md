---
description: 루프백 시나리오를 위한 클라이언트 인증서 인증
title: 루프백 시나리오를 위한 클라이언트 인증서 인증 | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: peterbae
ms.author: v-hyba
ms.openlocfilehash: bfc8816c30020669918b3632f94e289524097537
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438445"
---
# <a name="client-certificate-authentication-for-loopback-scenarios"></a>루프백 시나리오를 위한 클라이언트 인증서 인증

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

SQL Server 2016에 sp_execute_external_script(SPEES)라는 새 저장 프로시저가 추가되었습니다. 이 저장 프로시저를 사용하면 SQL Server가 확장 작업의 일부로 외부 스크립트를 SQL Server 외부에서 시작하고 실행할 수 있습니다. R 및 Python 스크립트에 대한 지원이 제공되며, 둘 다 JDBC 드라이버를 사용하여 SQL Server에 연결할 수 있는 라이브러리가 있습니다. Windows 기반 SQL Server는 Windows 통합 인증을 사용하여 쿼리를 시작한 사용자와 동일한 자격 증명으로 이러한 루프백 연결을 인증할 수 있지만, Linux SQL Server는 그렇게 할 수 없습니다. 따라서 사용자가 인증서 및 키를 사용하여 인증할 수 있도록 클라이언트 인증서 인증이 추가됩니다.

## <a name="connecting-using-client-certificate-authentication"></a>클라이언트 인증서 인증을 사용하여 연결

JDBC 드라이버는 이 기능에 대한 세 가지 연결 속성을 추가합니다.

* clientCertificate – 인증에 사용할 인증서를 지정합니다. JDBC 드라이버는 PFX, PEM, DER 및 CER 파일 확장을 지원합니다.

서식
```
clientCertificate=<file_location>
``` 
드라이버는 인증서 파일을 사용합니다. PEM, DER 및 CER 형식 인증서는 clientKey 특성이 필요합니다. 파일 위치는 상대 또는 절대 경로일 수 있습니다.
 
* clientKey - clientCertificate 특성에 지정된 PEM, DER 및 CER 인증서에 대해 프라이빗 키의 파일 위치를 지정합니다.

서식
```
clientKey=<file_location>
```
프라이빗 키 파일의 위치를 지정합니다. 프라이빗 키 파일이 암호로 보호되는 경우에는 암호 키워드가 필요합니다. 파일 위치는 상대 또는 절대 경로일 수 있습니다.

* clientKeyPassword – clientKey 파일의 프라이빗 키에 액세스하기 위해 제공되는 선택적 암호 문자열입니다.

이 기능은 Linux SQL Server 2019 이상에 대한 루프백 인증 시나리오에만 공식적으로 지원됩니다.

## <a name="see-also"></a>참고 항목

[JDBC 드라이버로 SQL Server에 연결](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
[sp_execute_external_script(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)
