# Jekyll Development Docker Image
FROM ruby:3.3.4-alpine

# Install system dependencies
RUN apk add --no-cache \
    build-base \
    git \
    nodejs \
    npm \
    tzdata

# Set working directory
WORKDIR /srv/jekyll

# Copy Gemfile and Gemfile.lock
COPY Gemfile Gemfile.lock ./

# Install Jekyll and dependencies
RUN bundle config set --local deployment 'true' && \
    bundle config set --local without 'development test' && \
    bundle install

# Copy the rest of the site
COPY . .

# Expose port 4000
EXPOSE 4000

# Default command
CMD ["bundle", "exec", "jekyll", "serve", "--host", "0.0.0.0", "--port", "4000"]