---
title: mssqlctl hdfs 참조
titleSuffix: SQL Server big data clusters
description: Mssqlctl hdfs 명령에 대 한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6a2044594065e6f98ed919ace2171279e6f72c25
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67957913"
---
# <a name="mssqlctl-hdfs"></a>mssqlctl hdfs

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에 대 한 참조를 제공 합니다 **hdfs** 명령에 **mssqlctl** 도구입니다. 다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[mssqlctl hdfs shell](#mssqlctl-hdfs-shell) | HDFS 셸은 HDFS 파일 시스템에 대 한 간단한 대화형 명령 셸입니다.
[mssqlctl hdfs ls](#mssqlctl-hdfs-ls) | 지정 된 파일 또는 디렉터리의 상태를 나열 합니다.
[mssqlctl hdfs 존재](#mssqlctl-hdfs-exists) | 파일이 나 디렉터리가 있는지 확인 합니다.  존재 하는 경우 True를 반환 하 고 False 그렇지 않은 경우.
[mssqlctl hdfs mkdir](#mssqlctl-hdfs-mkdir) | 지정된 된 경로에 디렉터리를 만듭니다.
[mssqlctl hdfs mv](#mssqlctl-hdfs-mv) | 지정된 된 위치에 지정 된 파일 또는 경로 이동 합니다.
[mssqlctl hdfs create](#mssqlctl-hdfs-create) | 지정된 된 위치에 텍스트 파일을 만듭니다.  데이터 매개 변수를 통해 간단한 텍스트 콘텐츠를 추가할 수 있습니다.
[읽을 mssqlctl hdfs](#mssqlctl-hdfs-read) | 파일의 콘텐츠를 읽습니다.  오프셋 및 길이 (바이트)는 선택적 매개 변수입니다.
[mssqlctl hdfs rm](#mssqlctl-hdfs-rm) | 파일 또는 디렉터리를 제거 합니다.
[mssqlctl hdfs rmr](#mssqlctl-hdfs-rmr) | 재귀적으로 파일 또는 디렉터리를 제거 합니다.
[mssqlctl hdfs chmod](#mssqlctl-hdfs-chmod) | 지정 된 파일 또는 디렉터리에 사용 권한을 변경 합니다.
[mssqlctl hdfs chown](#mssqlctl-hdfs-chown) | 소유자 또는 지정된 된 파일의 그룹을 변경 합니다.
## <a name="mssqlctl-hdfs-shell"></a>mssqlctl hdfs 셸
HDFS 셸은 HDFS 파일 시스템에 대 한 간단한 대화형 명령 셸입니다.
```bash
mssqlctl hdfs shell 
```
### <a name="examples"></a>예
셸을 시작 합니다.
```bash
mssqlctl hdfs shell
```
### <a name="global-arguments"></a>전역 인수
#### `--debug`
모든 디버그 로그 표시 로깅의 자세한 정도를 늘립니다.
#### `--help -h`
이 도움말 메시지 및 종료를 표시 합니다.
#### `--output -o`
출력 형식입니다.  허용 되는 값: json, jsonc, 테이블, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 참조 [ http://jmespath.org/ ](http://jmespath.org/]) 자세한 내용 및 예제에 대 한 합니다.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 사용-전체 디버그 로그에 대 한 디버그 합니다.
## <a name="mssqlctl-hdfs-ls"></a>mssqlctl hdfs ls
지정 된 파일 또는 디렉터리의 상태를 나열 합니다.
```bash
mssqlctl hdfs ls --path -p 
                 
```
### <a name="examples"></a>예
상태 나열
```bash
mssqlctl hdfs ls --path '/tmp'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
경로 목록 상태입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
모든 디버그 로그 표시 로깅의 자세한 정도를 늘립니다.
#### `--help -h`
이 도움말 메시지 및 종료를 표시 합니다.
#### `--output -o`
출력 형식입니다.  허용 되는 값: json, jsonc, 테이블, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 참조 [ http://jmespath.org/ ](http://jmespath.org/]) 자세한 내용 및 예제에 대 한 합니다.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 사용-전체 디버그 로그에 대 한 디버그 합니다.
## <a name="mssqlctl-hdfs-exists"></a>mssqlctl hdfs 존재
파일이 나 디렉터리가 있는지 확인 합니다.  존재 하는 경우 True를 반환 하 고 False 그렇지 않은 경우.
```bash
mssqlctl hdfs exists --path -p 
                     
```
### <a name="examples"></a>예
파일 또는 디렉터리가 있는지 확인 합니다.
```bash
mssqlctl hdfs exists --path '/tmp'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
확인할 수 있는지에 대 한 경로입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
모든 디버그 로그 표시 로깅의 자세한 정도를 늘립니다.
#### `--help -h`
이 도움말 메시지 및 종료를 표시 합니다.
#### `--output -o`
출력 형식입니다.  허용 되는 값: json, jsonc, 테이블, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 참조 [ http://jmespath.org/ ](http://jmespath.org/]) 자세한 내용 및 예제에 대 한 합니다.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 사용-전체 디버그 로그에 대 한 디버그 합니다.
## <a name="mssqlctl-hdfs-mkdir"></a>mssqlctl hdfs mkdir
지정된 된 경로에 디렉터리를 만듭니다.
```bash
mssqlctl hdfs mkdir --path -p 
                    
```
### <a name="examples"></a>예
디렉터리를 확인 합니다.
```bash
mssqlctl hdfs mkdir --path '/tmp'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
만들 디렉터리의 이름입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
모든 디버그 로그 표시 로깅의 자세한 정도를 늘립니다.
#### `--help -h`
이 도움말 메시지 및 종료를 표시 합니다.
#### `--output -o`
출력 형식입니다.  허용 되는 값: json, jsonc, 테이블, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 참조 [ http://jmespath.org/ ](http://jmespath.org/]) 자세한 내용 및 예제에 대 한 합니다.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 사용-전체 디버그 로그에 대 한 디버그 합니다.
## <a name="mssqlctl-hdfs-mv"></a>mssqlctl hdfs mv
지정된 된 위치에 지정 된 파일 또는 경로 이동 합니다.
```bash
mssqlctl hdfs mv --source-path -s 
                 --target-path -t
```
### <a name="examples"></a>예
파일 또는 디렉터리를 이동 합니다.
```bash
mssqlctl hdfs mv --source-path '/tmp' --target-path '/dest'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--source-path -s`
이동할 디렉터리입니다.
#### `--target-path -t`
이동할 위치입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
모든 디버그 로그 표시 로깅의 자세한 정도를 늘립니다.
#### `--help -h`
이 도움말 메시지 및 종료를 표시 합니다.
#### `--output -o`
출력 형식입니다.  허용 되는 값: json, jsonc, 테이블, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 참조 [ http://jmespath.org/ ](http://jmespath.org/]) 자세한 내용 및 예제에 대 한 합니다.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 사용-전체 디버그 로그에 대 한 디버그 합니다.
## <a name="mssqlctl-hdfs-create"></a>mssqlctl hdfs 만들기
지정된 된 위치에 텍스트 파일을 만듭니다.  데이터 매개 변수를 통해 간단한 텍스트 콘텐츠를 추가할 수 있습니다.
```bash
mssqlctl hdfs create --path -p 
                     --data -d
```
### <a name="examples"></a>예
파일을 만듭니다.
```bash
mssqlctl hdfs create --path '/tmp/test.txt' --data "This is a test."
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
만들 파일의 이름입니다.
#### `--data -d`
파일의 내용입니다.  간단한 텍스트 콘텐츠를 위한 것입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
모든 디버그 로그 표시 로깅의 자세한 정도를 늘립니다.
#### `--help -h`
이 도움말 메시지 및 종료를 표시 합니다.
#### `--output -o`
출력 형식입니다.  허용 되는 값: json, jsonc, 테이블, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 참조 [ http://jmespath.org/ ](http://jmespath.org/]) 자세한 내용 및 예제에 대 한 합니다.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 사용-전체 디버그 로그에 대 한 디버그 합니다.
## <a name="mssqlctl-hdfs-read"></a>읽을 mssqlctl hdfs
파일의 콘텐츠를 읽습니다.  오프셋 및 길이 (바이트)는 선택적 매개 변수입니다.
```bash
mssqlctl hdfs read --path -p 
                   --offset  
                   --length -l
```
### <a name="examples"></a>예
읽기 파일입니다.
```bash
mssqlctl hdfs read --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
읽을 파일의 이름입니다.
#### `--offset`
읽을 파일 내의 오프셋 바이트 수입니다.
#### `--length -l`
읽을 데이터의 길이입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
모든 디버그 로그 표시 로깅의 자세한 정도를 늘립니다.
#### `--help -h`
이 도움말 메시지 및 종료를 표시 합니다.
#### `--output -o`
출력 형식입니다.  허용 되는 값: json, jsonc, 테이블, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 참조 [ http://jmespath.org/ ](http://jmespath.org/]) 자세한 내용 및 예제에 대 한 합니다.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 사용-전체 디버그 로그에 대 한 디버그 합니다.
## <a name="mssqlctl-hdfs-rm"></a>mssqlctl hdfs rm
파일 또는 디렉터리를 제거 합니다.
```bash
mssqlctl hdfs rm --path -p 
                 
```
### <a name="examples"></a>예
파일 또는 디렉터리를 제거 합니다.
```bash
mssqlctl hdfs rm --path '/tmp'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
제거할 파일의 이름입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
모든 디버그 로그 표시 로깅의 자세한 정도를 늘립니다.
#### `--help -h`
이 도움말 메시지 및 종료를 표시 합니다.
#### `--output -o`
출력 형식입니다.  허용 되는 값: json, jsonc, 테이블, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 참조 [ http://jmespath.org/ ](http://jmespath.org/]) 자세한 내용 및 예제에 대 한 합니다.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 사용-전체 디버그 로그에 대 한 디버그 합니다.
## <a name="mssqlctl-hdfs-rmr"></a>mssqlctl hdfs rmr
재귀적으로 파일 또는 디렉터리를 제거 합니다.
```bash
mssqlctl hdfs rmr --path -p 
                  
```
### <a name="examples"></a>예
재귀 제거 디렉터리입니다.
```bash
mssqlctl hdfs rmr --path '/tmp'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
재귀적으로 제거 하려면 파일의 이름입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
모든 디버그 로그 표시 로깅의 자세한 정도를 늘립니다.
#### `--help -h`
이 도움말 메시지 및 종료를 표시 합니다.
#### `--output -o`
출력 형식입니다.  허용 되는 값: json, jsonc, 테이블, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 참조 [ http://jmespath.org/ ](http://jmespath.org/]) 자세한 내용 및 예제에 대 한 합니다.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 사용-전체 디버그 로그에 대 한 디버그 합니다.
## <a name="mssqlctl-hdfs-chmod"></a>mssqlctl hdfs chmod
지정 된 파일 또는 디렉터리에 사용 권한을 변경 합니다.
```bash
mssqlctl hdfs chmod --path -p 
                    --permission
```
### <a name="examples"></a>예
파일 또는 디렉터리 권한을 변경 합니다.
```bash
mssqlctl hdfs chmod --permission 775 --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
파일 또는 디렉터리에 사용 권한 설정의 이름입니다.
#### `--permission`
설정 하려면 권한 8 진수입니다.  "775" 예입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
모든 디버그 로그 표시 로깅의 자세한 정도를 늘립니다.
#### `--help -h`
이 도움말 메시지 및 종료를 표시 합니다.
#### `--output -o`
출력 형식입니다.  허용 되는 값: json, jsonc, 테이블, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 참조 [ http://jmespath.org/ ](http://jmespath.org/]) 자세한 내용 및 예제에 대 한 합니다.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 사용-전체 디버그 로그에 대 한 디버그 합니다.
## <a name="mssqlctl-hdfs-chown"></a>mssqlctl hdfs chown
소유자 또는 지정된 된 파일의 그룹을 변경 합니다.
```bash
mssqlctl hdfs chown --path -p 
                    --owner  
                    --group -g
```
### <a name="examples"></a>예
소유자와 그룹을 변경 합니다.
```bash
mssqlctl hdfs chown --owner hdfs --group superusergroup --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
소유자를 변경 하는 디렉터리나 파일의 이름입니다.
#### `--owner`
설정 하려면 소유자 이름입니다.
#### `--group -g`
그룹 이름 설정입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
모든 디버그 로그 표시 로깅의 자세한 정도를 늘립니다.
#### `--help -h`
이 도움말 메시지 및 종료를 표시 합니다.
#### `--output -o`
출력 형식입니다.  허용 되는 값: json, jsonc, 테이블, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 참조 [ http://jmespath.org/ ](http://jmespath.org/]) 자세한 내용 및 예제에 대 한 합니다.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 사용-전체 디버그 로그에 대 한 디버그 합니다.

## <a name="next-steps"></a>다음 단계

설치 하는 방법에 대 한 자세한 합니다 **mssqlctl** 도구를 참조 하십시오 [SQL Server 2019 빅 데이터 클러스터를 관리 하는 mssqlctl 설치](deploy-install-mssqlctl.md)합니다.