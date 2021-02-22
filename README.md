# SQL-ORACLE

/*

Trigger: 함수의 한종류
    촉발시키다. 스스로 발생하다.
    자동 호출되는 함수(CALL BACK)
    
    Trigger()
    
    Func()
    
    Trigger()
        before after
                    OLD NEW
            insert            0  
            delete      0   
            update      0   0
*/
```
SET SERVEROUTPUT ON

CREATE OR REPLACE TRIGGER trigger_test
    BEFORE 
        UPDATE ON departments
        --테이블을 고치려고 할때(업데이트 하기전에) 자동 호출된다
        FOR EACH ROW
        
        BEGIN
          ---  DBMS_OUTPUT.PUT_LINE('트리거 호출');
           DBMS_OUTPUT.PUT_LINE('변경전 컬럼의값 '||  :OLD.department_name);
           DBMS_OUTPUT.PUT_LINE('변경후 컬럼의값 '||  :NEW.department_name);
        END;
        /
        
        UPDATE DEPARTMENTS
        SET department_name = '정보기술'
        WHERE department_id = 300;
        
        
        ROLLBACK;-- 이전으로 되돌린다
        
 ```       
        
-- ROW 를 추가하는데 항상 평균 급여를 확인
CREATE OR REPLACE TRIGGER avg_trigger
    BEFORE -- AFTER T쓰면 추가된 이후에 출력된다
        INSERT OR UPDATE ON employees
        FOR EACH ROW
        
    ```  
    DECLARE
        avg_sal NUMBER;
    BEGIN
        SELECT ROUND(AVG(salary),2) INTO avg_sal
        FROM employees;
        DBMS_OUTPUT.PUT_LINE('급여평균 '|| avg_sal);
        
    END;
    /
    

    
    INSERT INTO employees(employee_id, last_name, hire_date, department_id, job_id,salary, email)
    VALUES(300,'Tiger',SYSDATE, 60,'IT_PROG',20000,'Tiger@naver.com');
    ```
        
    -- 수정되지 않도록 하는경우

```
CREATE OR REPLACE TRIGGER emp_tigger
    BEFORE
        UPDATE OR DELETE OR INSERT ON employees
        FOR EACH ROW
        
        BEGIN
            IF UPDATING THEN 
            IF :OLD.employee_id = '100' THEN
            RAISE_APPLICATION_ERROR(-20001, '이번호는 수정할 수 없습니다');
            END IF;
    END IF;
            
            
        END;
        /
        
        
        UPDATE employees
        SET salary = 2500
        WHERE employee_id = 100;
```
