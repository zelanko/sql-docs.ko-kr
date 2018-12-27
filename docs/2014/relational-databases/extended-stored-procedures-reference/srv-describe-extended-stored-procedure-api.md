---
title: srv_describe(확장 저장 프로시저 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- srv_describe
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_describe
ms.assetid: 2115600e-5ce7-4be0-9cd3-a1dd1fab0729
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 376aa2a01f6b7f25f29c1086c5ce0ea81fe87b14
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48096783"
---
# <a name="srvdescribe-extended-stored-procedure-api"></a>srv_describe(확장 저장 프로시저 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하세요.  
  
 행의 특정 열에 대해 열 이름과 원본 및 대상 데이터 형식을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
int srv_describe (  
SRV_PROC *  
srvproc  
,  
int  
colnumber  
,  
DBCHAR *  
column_name  
,  
int  
namelen  
,  
DBINT  
desttype  
,  
DBINT  
destlen  
,  
DBINT  
srctype  
,  
DBINT  
srclen  
,  
void *  
srcdata  
);  
  
```  
  
## <a name="arguments"></a>인수  
 *srvproc*  
 특정 클라이언트 연결에 대한 핸들(이 경우 행을 보내는 클라이언트)인 SRV_PROC 구조에 대한 포인터입니다. 이 구조에는 확장 저장 프로시저 API 라이브러리가 응용 프로그램과 클라이언트 간 통신 및 데이터를 관리하는 데 사용하는 모든 정보가 들어 있습니다.  
  
 *colnumber*  
 현재 지원되지 않습니다. 순서대로 열을 설명해야 합니다. **srv_sendrow**가 호출되기 전에 모든 열을 설명해야 합니다.  
  
 *column_name*  
 데이터가 속하는 열 이름을 지정합니다. 열에 이름이 없어도 되기 때문에 이 매개 변수는 NULL일 수 있습니다.  
  
 *namelen*  
 *column_name*의 길이(바이트)를 지정합니다. *namelen*이 SRV_NULLTERM이면 *column_name*이 null로 종결되어야 합니다.  
  
 *desttype*  
 대상 행 열의 데이터 형식을 지정합니다. 클라이언트로 전송되는 데이터 형식입니다. 데이터가 NULL인 경우에도 데이터 형식을 지정해야 합니다. 자세한 내용은 [데이터 형식(확장 저장 프로시저 API)](data-types-extended-stored-procedure-api.md)을 참조하세요.  
  
 *destlen*  
 클라이언트로 전송할 데이터의 길이(바이트)를 지정합니다. Null 값을 허용하지 않는 고정 길이 데이터 형식의 경우 *destlen*이 무시됩니다. Null 값을 허용하는 고정 길이 데이터 형식 및 가변 길이 데이터 형식의 경우 *destlen*은 대상 데이터의 최대 길이를 지정합니다.  
  
 *srctype*  
 원본 데이터의 데이터 형식을 지정합니다.  
  
 *srclen*  
 원본 데이터의 길이(바이트)를 지정합니다. 고정 길이 데이터 형식의 경우 이 값이 무시됩니다.  
  
 *srcdata*  
 특정 열에 대한 원본 데이터 주소를 제공합니다. **srv_sendrow**가 호출되면 *srcdata*에서 *colnumber*의 데이터를 찾습니다. 따라서 **srv_sendrow**를 호출하기 전에 해제하면 안 됩니다. **srv_setcoldata**를 사용하여 **srv_sendrow** 호출 사이에 원본 데이터 주소를 변경할 수 있습니다. **srv_setcoldata**에 대한 다른 호출에 의해 열 데이터가 바뀌거나 **srv_senddone**이 호출될 때까지 *srcdata*에 할당된 메모리를 해제하면 안 됩니다.  
  
 *desttype*이 SRVDECIMAL이나 SRVNUMERIC인 경우 *srcdata* 매개 변수는 구조의 전체 자릿수 및 소수 자릿수 필드가 원하는 값으로 설정되어 있는 DBNUMERIC 또는 DBDECIMAL 구조에 대한 포인터여야 합니다. DEFAULTPRECISION을 사용하여 기본 전체 자릿수를 지정하고 DEFAULTSCALE을 사용하여 기본 소수 자릿수를 지정할 수 있습니다.  
  
## <a name="returns"></a>반환 값  
 설명되는 열 번호입니다. 첫 번째 열은 열 1입니다. 오류가 발생하면 0이 반환됩니다.  
  
## <a name="remarks"></a>Remarks  
 **srv_sendrow**를 처음 호출하기 전에 행의 각 열에 대해 한 번씩, **srv_describe** 함수를 호출해야 합니다. 순서에 관계없이 행의 열을 설명할 수 있습니다.  
  
 전체 결과 집합이 전송되기 전에 열 행의 원본 데이터 위치와 길이를 변경하려면 각각 **srv_setcoldata** 및 **srv_setcollen**을 사용합니다.  
  
 데이터 형식 및 확장 저장 프로시저 API 데이터 형식 변환에 대한 설명은 [데이터 형식(확장 저장 프로시저 API)](data-types-extended-stored-procedure-api.md)을 참조하세요.  
  
 애플리케이션의 열 이름이 유니코드로 되어 있으면 **srv_describe**를 호출하기 전에 서버의 멀티바이트 코드 페이지로 변환해야 합니다. 자세한 내용은 [유니코드 데이터 및 서버 코드 페이지](../extended-stored-procedures-programming/unicode-data-and-server-code-pages.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [srv_sendrow(확장 저장 프로시저 API)](srv-sendrow-extended-stored-procedure-api.md)   
 [srv_setutype(확장 저장 프로시저 API)](srv-setutype-extended-stored-procedure-api.md)   
 [srv_setcoldata(확장 저장 프로시저 API)](srv-setcoldata-extended-stored-procedure-api.md)  
  
  
