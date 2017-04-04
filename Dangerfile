# Make it more obvious that a PR is a work in progress and shouldn't be merged yet
if github.pr_title.include? "WIP"
    warn("PR is classed as Work in Progress")
end

# Ensure a clean commits history
if git.commits.any? { |c| c.message =~ /^Merge branch/ }
  fail('Please rebase to get rid of the merge commits in this PR')
end

# Which parts of the repository did the PR touch?
has_build_system_changes = !git.modified_files.grep(/make-rules\/*.mk/).empty?
has_doc_changes = !git.modified_files.grep(/doc\//).empty?
has_transform_changes = !git.modified_files.grep(/transforms\//).empty?
has_tools_changes = !git.modified_files.grep(/tools\//).empty?
has_component_changes = !git.modified_files.grep(/components\//).empty?

# Checker functions
def check_depend_mk(file_name)
    return !`grep '^include.*depend.mk' #{file_name}`.empty?
end

def check_BUILD_PKG_DEPENDENCIES(file_name)
    return !`grep '^BUILD_PKG_DEPENDENCIES = .*' #{file_name}`.empty?
end

def check_required_packages(file_name)
    return `grep '^REQUIRED_PACKAGES \+= ' #{file_name}`.empty?
end

def check_ws_make_rules(file_name)
    return !`grep '^include .*' #{file_name} | grep -v 'shared-macros.mk' | grep '$(WS_MAKE_RULES)'`.empty?
end

def check_copyright(file_name)
    return !`grep '^# Copyright 2017 <contributor>' #{file_name}`.empty?
end

# Helper functions
def convert_to_link(file_name)
    return github.html_link(file_name)
end

def check_base_file(file_name)
    github.review.warn('Please add your copyright to ' + convert_to_link(file_name) if check_copyright(file_name))
end

def check_component_makefile(file_name)
    check_base_file(file_name)

    github.review.fail('Remove depend.mk line from ' + convert_to_link(file_name)) if check_depend_mk(file_name)
    github.review.fail('Remove BUILD_PKG_DEPENDENCIES line from ' + convert_to_link(file_name)) if check_BUILD_PKG_DEPENDENCIES(file_name)
    github.review.fail('Switch Makefile includes to use $(WS_MAKE_RULES) variable in ' + convert_to_link(file_name)) if check_ws_make_rules(file_name)
    github.review.warn('Consider adding REQUIRED_PACKAGES to ' + convert_to_link(file_name)) if check_required_packages(file_name)
end


github.review.start

# Component-related checks
if has_component_changes
    git.added_files.each do |file_name|
        is_dangerfile = file_name.match(/Dangerfile$/)
        is_component_makefile = file_name.match(/Makefile$/)
        is_component_ips_manifest = file_name.match(/.p5m$/)
        is_component_patch = file_name.match(/.patch$/)
        is_component_license = file_name.match(/.license$/)

        file_html_link = convert_to_link(file_name)

        if is_component_patch
            component_makefile = File.join(File.dirname(file_name), 'Makefile')
            github.review.fail('Bump COMPONENT_REVISION or COMPONENT_VERSION in ' + convert_to_link(component_makefile) + ' as new patch ' + file_html_link + ' was added')
        end
    end

    git.modified_files.each do |file_name|
	    is_travis_cfg = file_name.match(/^\.travis\.yml$/)
        is_dangerfile = file_name.match(/Dangerfile$/)
        is_vagrantfile = file_name.match(/Vagrantfile$/)
        is_component_makefile = file_name.match(/Makefile$/)
        is_component_ips_manifest = file_name.match(/.p5m$/)
        is_component_patch = file_name.match(/.patch$/)
        is_component_license = file_name.match(/.license$/)

        file_html_link = convert_to_link(file_name)

        if (is_travis_cfg || is_dangerfile || is_vagrantfile)
            github.review.message('This PR touches ' + file_html_link, sticky: false)
        end

        if is_component_makefile
            check_component_makefile(file_name)
            github.review.fail('Bump COMPONENT_REVISION or COMPONENT_VERSION in ' + file_html_link + ' as it was modified')
        end

        if is_component_ips_manifest
            component_makefile = File.join(File.dirname(file_name), 'Makefile')
            github.review.fail('Bump COMPONENT_REVISION or COMPONENT_VERSION in ' + convert_to_link(component_makefile) + ' as IPS manifest ' + file_html_link + ' was modified')
        end
    end

    git.deleted_files.each do |file_name|
        is_travis_cfg = file_name.match(/^\.travis\.yml$/)
        is_dangerfile = file_name.match(/Dangerfile$/)
        is_vagrantfile = file_name.match(/Vagrantfile$/)
        is_component_makefile = file_name.match(/Makefile$/)
        is_component_ips_manifest = file_name.match(/.p5m$/)
        is_component_patch = file_name.match(/.patch$/)
        is_component_license = file_name.match(/.license$/)

        file_html_link = convert_to_link(file_name)

        if (is_travis_cfg || is_dangerfile || is_vagrantfile)
            github.review.fail('Do not remove ' + File.basename(file_name), sticky: false)
        end

        if is_component_patch
            github.review.fail('Bump COMPONENT_REVISION or COMPONENT_VERSION as ' + file_html_link + ' was dropped')
        end
    end
end

github.review.submit
