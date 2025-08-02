#!/usr/bin/make -f
# Jekyll Development Makefile
# Comprehensive build system for Jekyll with GitHub Pages compatibility
# Author: Generated with Claude Code

# =============================================================================
# CONFIGURATION
# =============================================================================

# Project settings
SITE_URL := http://localhost:4000
JEKYLL_PORT := 4000
JEKYLL_HOST := 0.0.0.0

# Docker configuration
DOCKER_IMAGE := jekyll-site
DOCKER_CONTAINER := jekyll-dev
GITHUB_PAGES_IMAGE := github-pages-jekyll
GITHUB_PAGES_CONTAINER := github-pages-dev

# Docker Compose files
COMPOSE_FILE := docker-compose.yml
GITHUB_PAGES_COMPOSE := docker-compose.github-pages.yml

# Jekyll commands
JEKYLL_SERVE_CMD := jekyll serve --host $(JEKYLL_HOST) --port $(JEKYLL_PORT) --livereload
JEKYLL_SERVE_DOCKER_CMD := jekyll serve --host $(JEKYLL_HOST) --port $(JEKYLL_PORT) --livereload --force_polling
JEKYLL_BUILD_CMD := jekyll build
JEKYLL_BUILD_VERBOSE_CMD := jekyll build --verbose

# Docker run options
DOCKER_RUN_OPTS := --rm -v "$(PWD):/srv/jekyll"
DOCKER_RUN_SERVE_OPTS := $(DOCKER_RUN_OPTS) -p $(JEKYLL_PORT):$(JEKYLL_PORT)

# Colors for output
RESET := \033[0m
BOLD := \033[1m
RED := \033[31m
GREEN := \033[32m
YELLOW := \033[33m
BLUE := \033[34m
CYAN := \033[36m

# =============================================================================
# PHONY TARGETS
# =============================================================================

.PHONY: help \
	install serve build clean test \
	docker-build serve-docker build-docker docker-shell \
	serve-docker-official build-docker-official \
	compose-up compose-down compose-build compose-official \
	github-pages-build github-pages-serve github-pages-up github-pages-down github-pages-shell \
	dev docker-dev quick-serve compose-dev github-pages-dev \
	check-docker check-compose validate

# =============================================================================
# DEFAULT TARGET
# =============================================================================

.DEFAULT_GOAL := help

# =============================================================================
# HELP SYSTEM
# =============================================================================

help: ## Show this help message
	@echo "$(BOLD)$(CYAN)Jekyll Development Environment$(RESET)"
	@echo "$(CYAN)================================$(RESET)"
	@echo ""
	@echo "$(BOLD)QUICK START:$(RESET)"
	@echo "  $(GREEN)make github-pages-serve$(RESET)  $(YELLOW)# Recommended: GitHub Pages compatible$(RESET)"
	@echo "  $(GREEN)make serve$(RESET)               $(YELLOW)# Local development$(RESET)"
	@echo ""
	@echo "$(BOLD)LOCAL DEVELOPMENT:$(RESET)"
	@awk 'BEGIN {FS = ":.*##"; printf ""} /^[a-zA-Z_-]+:.*?##/ { if ($$1 ~ /^(install|serve|build|clean|test)$$/) printf "  $(GREEN)%-20s$(RESET) %s\n", $$1, $$2 }' $(MAKEFILE_LIST)
	@echo ""
	@echo "$(BOLD)GITHUB PAGES COMPATIBLE:$(RESET)"
	@awk 'BEGIN {FS = ":.*##"; printf ""} /^[a-zA-Z_-]+:.*?##/ { if ($$1 ~ /^github-pages/) printf "  $(GREEN)%-20s$(RESET) %s\n", $$1, $$2 }' $(MAKEFILE_LIST)
	@echo ""
	@echo "$(BOLD)DOCKER DEVELOPMENT:$(RESET)"
	@awk 'BEGIN {FS = ":.*##"; printf ""} /^[a-zA-Z_-]+:.*?##/ { if ($$1 ~ /^(docker-|serve-docker|build-docker)/ && $$1 !~ /github-pages/) printf "  $(GREEN)%-20s$(RESET) %s\n", $$1, $$2 }' $(MAKEFILE_LIST)
	@echo ""
	@echo "$(BOLD)DOCKER COMPOSE:$(RESET)"
	@awk 'BEGIN {FS = ":.*##"; printf ""} /^[a-zA-Z_-]+:.*?##/ { if ($$1 ~ /^compose/) printf "  $(GREEN)%-20s$(RESET) %s\n", $$1, $$2 }' $(MAKEFILE_LIST)
	@echo ""
	@echo "$(BOLD)SHORTCUTS:$(RESET)"
	@awk 'BEGIN {FS = ":.*##"; printf ""} /^[a-zA-Z_-]+:.*?##/ { if ($$1 ~ /^(dev|docker-dev|quick-serve|compose-dev|github-pages-dev)$$/) printf "  $(GREEN)%-20s$(RESET) %s\n", $$1, $$2 }' $(MAKEFILE_LIST)
	@echo ""
	@echo "$(BOLD)UTILITIES:$(RESET)"
	@awk 'BEGIN {FS = ":.*##"; printf ""} /^[a-zA-Z_-]+:.*?##/ { if ($$1 ~ /^(check-|validate)/) printf "  $(GREEN)%-20s$(RESET) %s\n", $$1, $$2 }' $(MAKEFILE_LIST)
	@echo ""
	@echo "$(YELLOW)Site will be available at: $(SITE_URL)$(RESET)"

# =============================================================================
# VALIDATION HELPERS
# =============================================================================

check-docker: ## Check if Docker is running
	@echo "$(CYAN)Checking Docker...$(RESET)"
	@docker info > /dev/null 2>&1 || (echo "$(RED)Error: Docker is not running. Please start Docker Desktop.$(RESET)" && exit 1)
	@echo "$(GREEN)✓ Docker is running$(RESET)"

check-compose: check-docker ## Check if Docker Compose is available
	@echo "$(CYAN)Checking Docker Compose...$(RESET)"
	@docker-compose --version > /dev/null 2>&1 || (echo "$(RED)Error: Docker Compose is not available.$(RESET)" && exit 1)
	@echo "$(GREEN)✓ Docker Compose is available$(RESET)"

validate: ## Validate environment and dependencies
	@echo "$(CYAN)Validating environment...$(RESET)"
	@command -v bundle > /dev/null 2>&1 || echo "$(YELLOW)Warning: Bundler not found. Local development may not work.$(RESET)"
	@command -v ruby > /dev/null 2>&1 || echo "$(YELLOW)Warning: Ruby not found. Local development may not work.$(RESET)"
	@[ -f Gemfile ] || (echo "$(RED)Error: Gemfile not found.$(RESET)" && exit 1)
	@[ -f _config.yml ] || (echo "$(RED)Error: _config.yml not found.$(RESET)" && exit 1)
	@echo "$(GREEN)✓ Environment validation complete$(RESET)"

# =============================================================================
# LOCAL DEVELOPMENT
# =============================================================================

install: validate ## Install Ruby dependencies locally
	@echo "$(CYAN)Installing Ruby dependencies...$(RESET)"
	@bundle install
	@echo "$(GREEN)✓ Dependencies installed$(RESET)"

serve: install ## Start Jekyll server locally (localhost:4000)
	@echo "$(CYAN)Starting Jekyll server locally...$(RESET)"
	@echo "$(YELLOW)Site will be available at $(SITE_URL)$(RESET)"
	@echo "$(YELLOW)Press Ctrl+C to stop the server$(RESET)"
	@bundle exec $(JEKYLL_SERVE_CMD)

build: install ## Build the site locally
	@echo "$(CYAN)Building Jekyll site locally...$(RESET)"
	@bundle exec $(JEKYLL_BUILD_CMD)
	@echo "$(GREEN)✓ Site built successfully$(RESET)"

clean: ## Clean generated files
	@echo "$(CYAN)Cleaning generated files...$(RESET)"
	@if command -v bundle > /dev/null 2>&1; then \
		bundle exec jekyll clean; \
	fi
	@rm -rf _site .jekyll-cache .sass-cache
	@echo "$(GREEN)✓ Cleanup complete$(RESET)"

test: install ## Test the site build with verbose output
	@echo "$(CYAN)Testing Jekyll site build...$(RESET)"
	@bundle exec $(JEKYLL_BUILD_VERBOSE_CMD)
	@echo "$(GREEN)✓ Build test successful$(RESET)"

# =============================================================================
# GITHUB PAGES COMPATIBLE DEVELOPMENT
# =============================================================================

github-pages-build: check-docker ## Build Docker image with exact GitHub Pages environment
	@echo "$(CYAN)Building Docker image with exact GitHub Pages environment...$(RESET)"
	@docker build -f Dockerfile.github-pages -t $(GITHUB_PAGES_IMAGE) .
	@echo "$(GREEN)✓ GitHub Pages image built$(RESET)"

github-pages-serve: github-pages-build ## Start Jekyll with exact GitHub Pages environment
	@echo "$(CYAN)Starting Jekyll with exact GitHub Pages environment...$(RESET)"
	@echo "$(YELLOW)Site will be available at $(SITE_URL)$(RESET)"
	@echo "$(YELLOW)Environment: Jekyll 3.10.0, Ruby 3.3.4 (matches GitHub Pages exactly)$(RESET)"
	@echo "$(YELLOW)Press Ctrl+C to stop the server$(RESET)"
	@docker run $(DOCKER_RUN_SERVE_OPTS) --name $(GITHUB_PAGES_CONTAINER) $(GITHUB_PAGES_IMAGE)

github-pages-up: check-compose ## Start GitHub Pages environment with Docker Compose
	@echo "$(CYAN)Starting GitHub Pages environment with Docker Compose...$(RESET)"
	@echo "$(YELLOW)Site will be available at $(SITE_URL)$(RESET)"
	@echo "$(YELLOW)Environment matches GitHub Pages exactly$(RESET)"
	@docker-compose -f $(GITHUB_PAGES_COMPOSE) up

github-pages-down: ## Stop GitHub Pages Docker Compose
	@echo "$(CYAN)Stopping GitHub Pages Docker Compose...$(RESET)"
	@docker-compose -f $(GITHUB_PAGES_COMPOSE) down
	@echo "$(GREEN)✓ GitHub Pages environment stopped$(RESET)"

github-pages-shell: github-pages-build ## Open shell in GitHub Pages environment
	@echo "$(CYAN)Opening shell in GitHub Pages environment...$(RESET)"
	@docker run $(DOCKER_RUN_OPTS) -it $(GITHUB_PAGES_IMAGE) /bin/bash

# =============================================================================
# DOCKER DEVELOPMENT
# =============================================================================

docker-build: check-docker ## Build the custom Docker image
	@echo "$(CYAN)Building custom Docker image...$(RESET)"
	@docker build -t $(DOCKER_IMAGE) .
	@echo "$(GREEN)✓ Docker image built$(RESET)"

serve-docker: docker-build ## Start Jekyll server using custom Docker image
	@echo "$(CYAN)Starting Jekyll server using custom Docker...$(RESET)"
	@echo "$(YELLOW)Site will be available at $(SITE_URL)$(RESET)"
	@echo "$(YELLOW)Press Ctrl+C to stop the server$(RESET)"
	@docker run $(DOCKER_RUN_SERVE_OPTS) --name $(DOCKER_CONTAINER) $(DOCKER_IMAGE) $(JEKYLL_SERVE_DOCKER_CMD)

build-docker: docker-build ## Build the site using custom Docker image
	@echo "$(CYAN)Building Jekyll site using custom Docker...$(RESET)"
	@docker run $(DOCKER_RUN_OPTS) $(DOCKER_IMAGE) $(JEKYLL_BUILD_CMD)
	@echo "$(GREEN)✓ Site built with Docker$(RESET)"

docker-shell: docker-build ## Open shell in custom Docker container
	@echo "$(CYAN)Opening shell in custom Docker container...$(RESET)"
	@docker run $(DOCKER_RUN_OPTS) -it $(DOCKER_IMAGE) /bin/bash

serve-docker-official: check-docker ## Start Jekyll server using official Docker image
	@echo "$(CYAN)Starting Jekyll server using official Docker image...$(RESET)"
	@echo "$(YELLOW)Site will be available at $(SITE_URL)$(RESET)"
	@echo "$(YELLOW)Press Ctrl+C to stop the server$(RESET)"
	@docker run $(DOCKER_RUN_SERVE_OPTS) --name $(DOCKER_CONTAINER) jekyll/jekyll:4 $(JEKYLL_SERVE_DOCKER_CMD)

build-docker-official: check-docker ## Build the site using official Docker image
	@echo "$(CYAN)Building Jekyll site using official Docker image...$(RESET)"
	@docker run $(DOCKER_RUN_OPTS) jekyll/jekyll:4 $(JEKYLL_BUILD_CMD)
	@echo "$(GREEN)✓ Site built with official Docker image$(RESET)"

# =============================================================================
# DOCKER COMPOSE DEVELOPMENT
# =============================================================================

compose-up: check-compose ## Start Jekyll using Docker Compose
	@echo "$(CYAN)Starting Jekyll using Docker Compose...$(RESET)"
	@echo "$(YELLOW)Site will be available at $(SITE_URL)$(RESET)"
	@docker-compose up jekyll

compose-down: ## Stop Docker Compose services
	@echo "$(CYAN)Stopping Docker Compose services...$(RESET)"
	@docker-compose down
	@echo "$(GREEN)✓ Docker Compose services stopped$(RESET)"

compose-build: check-compose ## Build and start using Docker Compose
	@echo "$(CYAN)Building and starting Jekyll using Docker Compose...$(RESET)"
	@echo "$(YELLOW)Site will be available at $(SITE_URL)$(RESET)"
	@docker-compose up --build jekyll

compose-official: check-compose ## Start Jekyll using official Docker image via Compose
	@echo "$(CYAN)Starting Jekyll using official Docker image via Compose...$(RESET)"
	@docker-compose up jekyll-official

# =============================================================================
# DEVELOPMENT SHORTCUTS
# =============================================================================

dev: serve ## Shortcut for local development
docker-dev: serve-docker ## Shortcut for Docker development
quick-serve: serve-docker-official ## Shortcut for quick Docker serve with official image
compose-dev: compose-up ## Shortcut for Docker Compose development
github-pages-dev: github-pages-serve ## Shortcut for GitHub Pages development

# =============================================================================
# UTILITY TARGETS
# =============================================================================

.SILENT: help install serve build clean test docker-build serve-docker build-docker docker-shell serve-docker-official build-docker-official compose-up compose-down compose-build compose-official github-pages-build github-pages-serve github-pages-up github-pages-down github-pages-shell dev docker-dev quick-serve compose-dev github-pages-dev check-docker check-compose validate