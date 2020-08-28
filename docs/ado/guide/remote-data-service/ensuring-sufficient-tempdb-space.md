---
description: 충분한 TempDB 공간 확인
title: TempDB 공간이 충분 한지 확인 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- TempDB space in RDS [ADO]
ms.assetid: 09130db1-6248-4234-a1e5-a9c8e1622c06
author: rothja
ms.author: jroth
ms.openlocfilehash: d6b93097b3a21e3858139146b50f15ddc79c6569
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978134"
---
# <a name="ensuring-sufficient-tempdb-space"></a>충분한 TempDB 공간 확인
Microsoft SQL Server 6.5에서 처리 공간이 필요한 [레코드 집합](../../reference/ado-api/recordset-object-ado.md) 개체를 처리 하는 동안 오류가 발생 하는 경우 TempDB의 크기를 늘려야 할 수 있습니다. 일부 쿼리에는 임시 처리 공간이 필요 합니다. 예를 들어 ORDER BY 절을 사용 하는 쿼리에는 약간의 임시 공간이 필요한 **레코드 집합**정렬이 필요 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
> [!IMPORTANT]
>  확장 된 후에는 장치를 축소 하기가 쉽지 않기 때문에 작업을 수행 하기 전에이 절차를 참조 하세요.  
  
> [!NOTE]
>  기본적으로 Microsoft SQL Server 7.0 이상에서는 TempDB가 필요에 따라 자동으로 증가 하도록 설정 되어 있습니다. 따라서 7.0 이전 버전을 실행 하는 서버 에서만이 절차가 필요할 수 있습니다.  
  
### <a name="to-increase-the-tempdb-space-on-sql-server-65"></a>SQL Server 6.5에서 TempDB 공간을 늘리려면  
  
1.  Microsoft SQL Server Enterprise Manager를 시작 하 고 서버의 트리를 연 다음 데이터베이스 장치 트리를 엽니다.  
  
2.  확장할 (물리적) 장치 (예: 마스터)를 선택 하 고 장치를 두 번 클릭 하 여 **데이터베이스 장치 편집** 대화 상자를 엽니다.  
  
     이 대화 상자에는 현재 데이터베이스에서 사용 중인 공간의 양이 표시 됩니다.  
  
3.  **크기** 상자에서 원하는 크기 (예: 50 메가바이트 (mb)의 하드 디스크 공간)로 장치를 늘립니다.  
  
4.  (논리) TempDB를 확장할 수 있는 공간의 크기를 늘리려면 **지금 변경** 을 클릭 합니다.  
  
5.  서버에서 데이터베이스 트리를 열고 **TempDB** 를 두 번 클릭 하 여 **데이터베이스 편집** 대화 상자를 엽니다. **데이터베이스** 탭은 TempDB (**데이터 크기**)에 현재 할당 된 공간의 크기를 나열 합니다. 기본적으로이 크기는 2mb입니다.  
  
6.  **크기** 그룹에서 **확장**을 클릭 합니다. 그래프는 각 물리적 장치에서 사용 가능한 공간 및 할당 된 공간을 보여 줍니다. 적갈색 막대는 사용 가능한 공간을 나타냅니다.  
  
7.  Master와 같은 **로그 장치**를 선택 하 여 **크기 (MB)** 상자에 사용 가능한 크기를 표시 합니다.  
  
8.  **지금 확장** 을 클릭 하 여 TempDB 데이터베이스에 해당 공간을 할당 합니다.  
  
     **데이터베이스 편집** 대화 상자에 TempDB에 대 한 새 할당 된 크기가 표시 됩니다.  
  
 이 항목에 대 한 자세한 내용은 "데이터베이스 확장 대화 상자"에 대 한 Microsoft SQL Server Enterprise Manager 도움말 파일을 검색 하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [RDS 기본 사항](./rds-fundamentals.md)