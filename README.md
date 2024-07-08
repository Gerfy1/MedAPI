# API REST para Consultório Médico

Este projeto desenvolve uma API REST para gerenciar operações em um consultório médico, abrangendo tanto o lado do cliente quanto do servidor, e integrando ambos. Durante o desenvolvimento foram aplicadas as seguintes tecnologias e práticas:

## Tecnologias e Práticas Utilizadas

- **DTO (Data Transfer Object)**: Utilização de DTOs para estruturar os dados transferidos entre cliente e servidor.
  
- **Integração com Banco de Dados**: Implementação de conexão com banco de dados para armazenamento e recuperação de dados.

- **Flyway**: Utilização do Flyway para controle de versão e migração de banco de dados.

- **Requisições HTTP (GET, PUT, DELETE, POST)**: Implementação de endpoints RESTful para realizar operações de leitura, atualização, exclusão e criação de recursos.

- **Beans**: Uso de beans gerenciados pelo Spring Framework para injeção de dependências e gerenciamento de componentes.

- **Spring Security e JWT (Auth0)**: Implementação de segurança utilizando Spring Security com autenticação baseada em JWT (JSON Web Tokens) do Auth0.

- **Spring Doc (Swagger)**: Utilização do Spring Doc (integrado com Swagger) para documentação automática da API, facilitando a visualização e teste dos endpoints.

- **Fluxo Given/When/Then**: Adoção do padrão Given/When/Then nos testes para estruturar e organizar cenários de testes automatizados.

- **Testes Unitários com JUnit e AssertJ**: Implementação de testes unitários utilizando JUnit para escrever e executar testes, e AssertJ para fazer asserções de forma fluente.

- **Mockito**: Utilização do Mockito para criar mocks e simular comportamentos de dependências durante os testes.

Este projeto visa demonstrar a aplicação prática dessas tecnologias e práticas no contexto de desenvolvimento de APIs RESTful para aplicações corporativas.

## Exemplo de Código

```java
@RestController
@RequestMapping("/pacientes")
public class PacienteController {

    @Autowired
    private PacienteService pacienteService;

    @GetMapping("/{id}")
    public ResponseEntity<PacienteDTO> getPaciente(@PathVariable Long id) {
        PacienteDTO paciente = pacienteService.findById(id);
        return ResponseEntity.ok(paciente);
    }

    @PostMapping
    public ResponseEntity<Void> createPaciente(@RequestBody PacienteDTO pacienteDTO) {
        pacienteService.create(pacienteDTO);
        return ResponseEntity.status(HttpStatus.CREATED).build();
    }

    @PutMapping("/{id}")
    public ResponseEntity<Void> updatePaciente(@PathVariable Long id, @RequestBody PacienteDTO pacienteDTO) {
        pacienteService.update(id, pacienteDTO);
        return ResponseEntity.noContent().build();
    }

    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deletePaciente(@PathVariable Long id) {
        pacienteService.delete(id);
        return ResponseEntity.noContent().build();
    }
}
