-- 1. Tabela de Usuários (Acessam o sistema)
CREATE TABLE usuarios (  
    id INT AUTO_INCREMENT PRIMARY KEY,  
    nome VARCHAR(100) NOT NULL,  
    email VARCHAR(100) NOT NULL UNIQUE,  
    senha VARCHAR(255) NOT NULL,  
    perfil ENUM('admin', 'atendente') DEFAULT 'atendente',  
    status ENUM('ativo', 'inativo') DEFAULT 'ativo',  
    criado_em TIMESTAMP DEFAULT CURRENT_TIMESTAMP  
); 

-- 2. Tabela de Pessoas (Alunos ou pessoas atendidas)
CREATE TABLE pessoas (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    cpf VARCHAR(14) NOT NULL UNIQUE,
    endereco VARCHAR(255),
    criado_em TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- 3. Tabela de Tipos de Atendimentos (Categorias)
CREATE TABLE tipos_atendimentos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL UNIQUE, -- Ex: "Matrícula", "Suporte Financeiro", "Pedagógico"
    descricao TEXT,
    ativo BOOLEAN DEFAULT TRUE,
    criado_em TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- 4. Tabela de Atendimentos (Registros dos atendimentos realizados)
CREATE TABLE atendimentos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    pessoa_id INT NOT NULL,           -- Quem foi atendido
    usuario_id INT NOT NULL,          -- Quem realizou o atendimento (atendente/admin)
    tipo_atendimento_id INT NOT NULL, -- Qual era a categoria do atendimento
    descricao_atendimento TEXT NOT NULL,
    status ENUM('em_andamento', 'finalizado', 'cancelado') DEFAULT 'em_andamento',
    data_atendimento TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    
    -- Relacionamentos (Chaves Estrangeiras)
    FOREIGN KEY (pessoa_id) REFERENCES pessoas(id),
    FOREIGN KEY (usuario_id) REFERENCES usuarios(id),
    FOREIGN KEY (tipo_atendimento_id) REFERENCES tipos_atendimentos(id)
);
