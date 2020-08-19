---
description: DataFactory 사용자 지정
title: DataFactory 사용자 지정 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory customization in RDS [ADO]
ms.assetid: 86d77985-a0d0-405a-8587-c85a20540a0e
author: rothja
ms.author: jroth
ms.openlocfilehash: b7ec3707df187e09de92fa42d7ed2b1c1b8e1130
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452225"
---
# <a name="datafactory-customization"></a>DataFactory 사용자 지정
RDS (원격 데이터 서비스)는 3 계층 클라이언트/서버 시스템에서 데이터 액세스를 쉽게 수행할 수 있는 방법을 제공 합니다. 클라이언트 데이터 컨트롤은 원격 데이터 원본에 대 한 쿼리를 수행 하는 연결 및 명령 문자열 매개 변수 또는 업데이트를 수행 하기 위해 연결 문자열 및 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 매개 변수를 지정 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
 매개 변수는 원격 데이터 원본에 대 한 데이터 액세스 작업을 수행 하는 서버 프로그램에 전달 됩니다. RDS는 [RDSServer DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 개체 라는 기본 서버 프로그램을 제공 합니다. **RDSServer** 개체는 쿼리에 의해 생성 된 모든 **레코드 집합** 개체를 클라이언트에 반환 합니다.  
  
 그러나 **RDSServer. DataFactory** 는 쿼리 및 업데이트를 수행 하는 것으로 제한 됩니다. 연결 또는 명령 문자열에 대 한 유효성 검사 나 처리를 수행할 수 없습니다.  
  
 ADO를 사용 하면 **DataFactory** 가 *처리기*라는 다른 유형의 서버 프로그램과 함께 작동 하도록 지정할 수 있습니다. 처리기는 데이터 원본에 액세스 하는 데 사용 되기 전에 클라이언트 연결 및 명령 문자열을 수정할 수 있습니다. 또한 처리기는 데이터 원본에 대 한 데이터를 읽고 쓰는 클라이언트의 기능을 제어 하는 액세스 권한을 적용할 수 있습니다.  
  
 처리기가 클라이언트 매개 변수 및 액세스 권한을 수정 하는 데 사용 하는 매개 변수는 사용자 지정 파일의 섹션에서 지정 합니다.  
  
 다음 항목에서는 **DataFactory** 개체를 사용자 지정 하는 방법에 대 한 자세한 정보를 제공 합니다.  
  
-   [사용자 지정 파일 이해](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)  
  
-   [사용자 지정 파일 연결 섹션](../../../ado/guide/remote-data-service/customization-file-connect-section.md)  
  
-   [사용자 지정 파일 SQL 섹션](../../../ado/guide/remote-data-service/customization-file-sql-section.md)  
  
-   [사용자 지정 파일 UserList 섹션](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)  
  
-   [사용자 지정 파일 로그 섹션](../../../ado/guide/remote-data-service/customization-file-logs-section.md)  
  
-   [필수 클라이언트 설정](../../../ado/guide/remote-data-service/required-client-settings.md)  
  
-   [고유한 사용자 지정된 처리기 작성](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


