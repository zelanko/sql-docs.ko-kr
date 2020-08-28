---
description: ConvertToString 메서드(RDS)
title: ConvertToString 메서드 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ConvertToString method [ADO]
ms.assetid: b3f36bc8-6f69-49b0-83cd-2ccd3afebfbe
author: rothja
ms.author: jroth
ms.openlocfilehash: 6f0d262e3ffeee6b5c5fecf32a12f89a5b5b8c12
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88982624"
---
# <a name="converttostring-method-rds"></a>ConvertToString 메서드(RDS)
[레코드 집합을 레코드](../ado-api/recordset-object-ado.md) 집합 데이터를 나타내는 MIME 문자열로 변환 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DataFactory.ConvertToString(Recordset)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DataFactory*  
 DataFactory 개체를 나타내는 개체 변수 [RDSServer](./datafactory-object-rdsserver.md) .  
  
 *레코드 집합*  
 **레코드 집합** 개체를 나타내는 개체 변수입니다.  
  
## <a name="remarks"></a>설명  
 .Asp 파일을 사용 하면 **Converttostring** 을 사용 하 여 서버에서 생성 된 HTML 페이지에 **레코드 집합** 을 포함 하 여 클라이언트 컴퓨터로 전송 합니다.  
  
 **Converttostring** 은 먼저 커서 서비스 테이블에 **레코드 집합** 을 로드 한 다음 MIME 형식으로 스트림을 생성 합니다.  
  
 클라이언트에서 원격 데이터 서비스는 MIME 문자열을 완전히 작동 하는 **레코드 집합**으로 다시 변환할 수 있습니다. 행 당 1024 바이트 이하의 데이터 행을 400 처리 하는 데 적합 합니다. HTTP를 통해 BLOB 데이터 및 대량 결과 집합을 스트리밍하는 데 사용할 수 없습니다. 문자열에 대해 실시간 압축을 수행 하지 않으므로 원격 데이터 서비스에서 기본 전송 프로토콜 형식으로 정의 하 고 배포 하는 유선 최적화 tablegram 형식에 비해 매우 큰 데이터 집합은 HTTP를 통해 전송 하는 데 상당한 시간이 걸립니다.  
  
> [!NOTE]
>  Active Server 페이지를 사용 하 여 결과 MIME 문자열을 클라이언트 HTML 페이지에 포함 하는 경우 버전 2.0 이전 VBScript 버전은 문자열의 크기를 32K로 제한 합니다. 이 제한을 초과 하면 오류가 반환 됩니다. .Asp 파일을 통해 MIME 포함을 사용할 때 쿼리 범위를 상대적으로 작게 유지 합니다. 이 문제를 해결 하려면 Microsoft Windows 스크립트 기술 웹 사이트에서 VBScript의 최신 버전을 다운로드 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataFactory 개체(RDSServer)](./datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>참고 항목  
 [ConvertToString 메서드 예제 (VB)](../ado-api/converttostring-method-example-vb.md)   
 [ConvertToString 메서드 예제(VBScript)](./converttostring-method-example-vbscript.md)