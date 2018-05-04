---
title: 사용자 지정 DataFactory | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory customization in RDS [ADO]
ms.assetid: 86d77985-a0d0-405a-8587-c85a20540a0e
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 174cc584b0f1ca89627dffcd3f85bb4a5f384229
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="datafactory-customization"></a>DataFactory 사용자 지정
원격 데이터 서비스 (RDS) 3 계층 클라이언트/서버 시스템에서 데이터 액세스를 쉽게 수행 하는 방법을 제공 합니다. 클라이언트 데이터 컨트롤의 원격 데이터 원본 또는 연결 문자열에서 쿼리를 수행 하려면 연결 및 명령 문자열 매개 변수를 지정 하 고 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 업데이트를 수행 하려면 매개 변수 개체입니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 매개 변수는 원격 데이터 원본에서 데이터 액세스 작업을 수행 하는 서버 프로그램에 전달 됩니다. 호출 하는 기본 서버 프로그램을 제공 하는 RDS는 [업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 개체입니다. **업데이트할** 개체 반환 **레코드 집합** 클라이언트에는 쿼리에 의해 생성 된 개체입니다.  
  
 그러나는 **업데이트할** 쿼리 및 업데이트를 수행 하도록 제한 됩니다. 연결 또는 명령 문자열에서 모든 유효성 검사 또는 처리를 수행할 수 없습니다 것입니다.  
  
 ADO를 사용 하는 지정할 수 있습니다는 **DataFactory** 함께 다른 유형의 서버 프로그램 라는 회사는 *처리기*합니다. 데이터 원본에 액세스 하는 사용 하기 전에 처리기 클라이언트 연결 및 명령 문자열을 수정할 수 있습니다. 또한 처리기를 읽고 데이터 소스에 데이터를 쓰는 클라이언트의 기능을 제어 하는 액세스 권한을 적용할 수 있습니다.  
  
 처리기가 클라이언트 매개 변수를 수정 하 고 권한 액세스를 사용 하는 매개 변수는 사용자 지정 파일의 섹션에 지정 됩니다.  
  
 다음 항목에서는 사용자 지정 하는 방법에 대 한 자세한 정보는 **DataFactory** 개체입니다.  
  
-   [사용자 지정 파일 이해](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)  
  
-   [사용자 지정 파일 연결 섹션](../../../ado/guide/remote-data-service/customization-file-connect-section.md)  
  
-   [사용자 지정 파일 SQL 섹션](../../../ado/guide/remote-data-service/customization-file-sql-section.md)  
  
-   [사용자 지정 파일 UserList 섹션](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)  
  
-   [사용자 지정 파일 로그 섹션](../../../ado/guide/remote-data-service/customization-file-logs-section.md)  
  
-   [필수 클라이언트 설정](../../../ado/guide/remote-data-service/required-client-settings.md)  
  
-   [고유한 사용자 지정된 처리기 작성](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


