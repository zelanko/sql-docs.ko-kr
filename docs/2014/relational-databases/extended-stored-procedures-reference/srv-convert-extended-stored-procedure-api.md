---
title: srv_convert(확장 저장 프로시저 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_convert
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_convert
ms.assetid: 216b4a31-786e-4361-8a33-e5f6e9790f90
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6bc430354ca8ef220caed882f1f8c7942b44d158
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63127275"
---
# <a name="srv_convert-extended-stored-procedure-api"></a>srv_convert(확장 저장 프로시저 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]대신 CLR 통합을 사용 하세요.  
  
 한 데이터 형식에서 다른 데이터 형식으로 데이터를 변경합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
int srv_convert (  
SRV_PROC *  
srvproc  
,  
int  
srctype  
,  
void *  
src  
,  
DBINT  
srclen  
,  
int  
desttype  
,  
void *  
dest  
,  
DBINT  
destlen  
);  
  
```  
  
## <a name="arguments"></a>인수  
 *srvproc*  
 특정 클라이언트 연결에 대한 핸들인 SRV_PROC 구조에 대한 포인터입니다. 이 구조에는 확장 저장 프로시저 API가 애플리케이션과 클라이언트 간 통신 및 데이터를 관리하는 데 사용하는 모든 제어 정보가 들어 있습니다. 
  *srvproc* 핸들을 제공하면 오류가 발생할 경우 확장 저장 프로시저 API 오류 처리기로 해당 핸들이 전달됩니다.  
  
 *중 유형이*  
 변환할 데이터의 데이터 형식을 지정합니다. 이 매개 변수는 임의의 확장 저장 프로시저 API 데이터 형식일 수 있습니다.  
  
 *소스*  
 변환할 데이터에 대한 포인터입니다. 이 매개 변수는 임의의 확장 저장 프로시저 API 데이터 형식일 수 있습니다.  
  
 *srclen*  
 변환할 데이터의 길이(바이트)를 지정합니다. 
  *srclen*이 0이면 **srv_convert**는 대상 변수에 Null 값을 넣습니다. 0이 아니면 고정 길이 데이터 형식의 경우 이 매개 변수가 무시되며, 이때 원본 데이터는 NULL인 것으로 가정됩니다. SRVCHAR 데이터 형식의 데이터에서 길이 -1은 문자열이 Null로 종결됨을 나타냅니다.  
  
 *desttype*  
 원본을 변환할 데이터 형식을 지정합니다. 이 매개 변수는 임의의 확장 저장 프로시저 API 데이터 형식일 수 있습니다.  
  
 *dest*  
 변환된 데이터를 받는 대상 변수에 대한 포인터입니다. 이 포인터가 NULL이면 **srv_convert**에서 사용자가 제공한 오류 처리기(있는 경우)를 호출하고 -1을 반환합니다.  
  
 
  *desttype*이 SRVDECIMAL이나 SRVNUMERIC인 경우 *dest* 매개 변수는 구조의 전체 자릿수 및 소수 자릿수 필드가 원하는 값으로 설정되어 있는 DBNUMERIC 또는 DBDECIMAL 구조에 대한 포인터여야 합니다. DEFAULTPRECISION을 사용하여 기본 전체 자릿수를 지정하고 DEFAULTSCALE을 사용하여 기본 소수 자릿수를 지정할 수 있습니다.  
  
 *destlen*  
 대상 변수의 길이(바이트)를 지정합니다. 고정 길이 데이터 형식의 경우 이 매개 변수가 무시됩니다. SRVCHAR 유형의 대상 변수에서 *destlen* 값은 대상 버퍼 공간의 총 길이여야 합니다. SRVCHAR 또는 SRVBINARY 유형의 대상 변수에서 길이 -1은 사용 가능한 충분한 공간이 있음을 나타냅니다. 
  *srvchar* 유형의 대상 변수에서 길이가 -1이면 문자열이 Null로 종결됩니다.  
  
## <a name="returns"></a>반환  
 데이터 형식 변환에 성공할 경우 변환된 데이터의 길이(바이트)입니다. 
  **srv_convert**에서 지원하지 않는 변환 요청을 발견하면 개발자가 제공한 오류 처리기(있는 경우)를 호출하며, 전역 오류 번호를 설정하고 -1을 반환합니다.  
  
## <a name="remarks"></a>설명  
 
  **srv_willconvert** 함수는 특정 변환의 허용 여부를 결정합니다.  
  
 근사치 데이터 형식 SRVFLT4 또는 SRVFLT8로 변환하면 전체 자릿수 손실이 발생할 수 있습니다. 근사치 데이터 형식 SRVFLT4 또는 SRVFLT8을 SRVCHAR 또는 SRVTEXT로 변환하는 경우에도 전체 자릿수 손실이 발생할 수 있습니다.  
  
 SRVFLT*x*, SRVINT*x*, SRVMONEY, SRVMONEY4, SRVDECIMAL 또는 SRVNUMERIC으로 변환하면 숫자가 대상의 최대값보다 클 경우 오버플로가 발생하고, 숫자가 대상의 최소값보다 작을 경우 언더플로가 발생할 수 있습니다. SRVCHAR 또는 SRVTEXT로 변환할 때 오버플로가 발생하면 결과 값의 첫 문자에 오류를 나타내는 별표(*)가 포함됩니다.  
  
 SRVCHAR를 SRVBINARY로 변환하는 경우 **srv_convert**는 문자열에 선행 0이 포함되어 있는지 여부에 관계없이 SRVCHAR를 16진수로 해석합니다. SRVBINARY를 SRVCHAR로 변환하는 경우에는 **srv_convert**에서 선행 0 없이 16진수 문자열을 만듭니다. 다른 모든 경우에서 SRVBINARY 데이터 형식과의 변환은 단순한 비트 복사입니다.  
  
 경우에 따라 데이터 형식을 동일한 데이터 형식으로 변환하는 것이 유용할 수 있습니다. 예를 들어 *destlen*을 -1로 설정하여 SRVCHAR를 SRVCHAR로 변환하면 문자열에 Null 종결자가 추가됩니다.  
  
 데이터 형식 및 확장 저장 프로시저 API 데이터 형식 변환에 대한 설명은 [데이터 형식(확장 저장 프로시저 API)](data-types-extended-stored-procedure-api.md)을 참조하세요.  
  
 
  **srv_convert** 함수는 여러 가지 이유로 실패할 수 있습니다.  
  
-   요청된 변환을 사용할 수 없습니다.  
  
-   변환으로 인해 대상 변수에서 잘림, 오버플로 또는 전체 자릿수 손실이 발생했습니다.  
  
-   문자열을 숫자 데이터 형식으로 변환하는 동안 구문 오류가 발생했습니다.  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [srv_setutype &#40;확장 저장 프로시저 API&#41;](srv-setutype-extended-stored-procedure-api.md)   
 [srv_willconvert &#40;확장 저장 프로시저 API&#41;](srv-willconvert-extended-stored-procedure-api.md)  
  
  
