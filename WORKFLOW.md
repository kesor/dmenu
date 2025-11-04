# DMENU Development Workflow

This follows the same workflow as DWM. See the main workflow documentation:

**[DWM/DMENU Workflow Documentation](../dwm/WORKFLOW.md)**

## DMENU-Specific Details

- **Repository:** `~/src/suckless/dmenu/`
- **Remote:** `git@github.com:kesor/dmenu.git`
- **Branch:** `master-patched`
- **Personal patch:** `kesor-personalization.diff`

## Package Locations

**Home Manager:** `~/src/dotfiles/config-nix-hm/modules/gui/wm/dwm/default.nix`
- Look for `patched-dmenu` definition

**NixOS:** Check if separate dmenu package exists in nixos modules

## Quick Commands

```bash
# Start workflow
cd ~/src/suckless/dmenu && quilt push -a

# Test build  
nix-shell -p gcc xorg.libX11 xorg.libXft xorg.libXinerama freetype fontconfig --run "make clean && make"

# Save and commit
quilt refresh && quilt pop -a
git add patches/kesor-personalization.diff
git commit -m "Description"
git push kesor master-patched

# Update packages with new commit hash
git rev-parse HEAD
nix-shell -p nix-prefetch-github --run "nix-prefetch-github kesor dmenu --rev COMMIT_HASH"
```
