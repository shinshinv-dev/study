> @RequiredArgsConstructor (lombok)
- final이 붙거나 @NotNull 이 붙은 필드의 생성자를 자동 생성해주는 롬복 어노테이션

> @Data (lombok)
- @Getter, @Setter, @RequiredArgsConstructor, @ToString, @EqualsAndHashCode을 한꺼번에 설정

> @NoArgsConstructor
- 파라미터가 없는 기본 생성자 생성

> @AllArgsConstructor
- 모든 필드 값을 파라미터로 받는 생성자 생성

> @RestControllerAdvice
- @ExceptionHandler, @ModelAttribute, @InitBinder 가 적용된 메서드들에 AOP를 적용해 Controller 단에 적용하기 위해 고안된 어노테이션
- 클래스에 선언하면 되며, 모든 @Controller에 대한, 전역적으로 발생할 수 있는 예외를 잡아서 처리 가능
- @ControllerAdvice + @ResponseBody
